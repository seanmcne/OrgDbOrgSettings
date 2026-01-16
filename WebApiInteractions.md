# OrgDbOrgSettings - WebAPI Interactions Summary

This document explains how the OrgDbOrgSettings solution manages organization.orgdborgsettings using the WebAPI.

---

## Dataverse API Endpoint

All operations use the same endpoint pattern: 

```
[OrgRootUrl]/api/data/v[version]/organizations([organizationId])
```

**HTTP Method:** `PATCH` (for all create/update/delete operations)

---

## READ Settings

**Solution Javascript Function name:** `getOrganizationEntityFromCrmWebApi()`

**HTTP Request:**
```
GET /api/data/v[version]/organizations
```

**Process:**
- Retrieves the entire Organization entity
- The `orgdborgsettings` field contains XML with all settings
- Parses the XML to populate the settings collection in the UI

---

## UPDATE/ADD a Setting

**Solution Javascript Function name:** `updateOrgDbOrgSettingOnServer(orgDbOrgSettingXml, organizationId, ... )`

**HTTP Request:**
```
PATCH /organizations(organizationId)
Body: { "orgdborgsettings": "<orgSettings>...</orgSettings>" }
```

**Process:**

1. User modifies a setting value in the UI
2. A clone of the setting object is created
3. The new value is validated against min/max constraints
4. The setting is serialized to XML format:  `<SettingName>value</SettingName>`
5. Wrapped in `<orgSettings>` tags
6. PATCH request sends the full updated XML blob

### For Organization Attributes

Organization Attributes are special settings stored as actual entity columns (not in the XML blob).

**Solution Javascript Function name:** `setOrganizationAttributeValue(attributeName, attributeValue, organizationId)`

**HTTP Request:**
```
PATCH /organizations(organizationId)
Body: { "attributename": attributeValue }
```

This updates the attribute directly on the organization entity. 

---

## DELETE a Setting

**Solution Javascript Function name:** `deleteSetting(strSettingToDelete)`

> **Important:** There is no direct DELETE operation. Instead, the solution uses a **two-step PATCH** process. 

### Step 1: Clear All Settings

```
PATCH /organizations(organizationId)
Body: { "orgdborgsettings":  "" }
```

This sends an empty string to clear all settings.

### Step 2: Rebuild Without the Deleted Setting

```javascript 
// Loop through all settings EXCEPT the one being deleted
// rebuilds all the settings in javascript to be submitted
forEach(setting) {
    if (setting.name != strSettingToDelete) {
        finalXmlUpdate += setting.toRawXmlSetting();
    }
}
```

```
PATCH /organizations(organizationId)
Body: { "orgdborgsettings": "<orgSettings>... all settings except deleted one...</orgSettings>" }
```

### Why This Approach?

- The `orgdborgsettings` field is a single XML blob containing ALL settings
- You cannot remove individual settings from it directly (historically this was true, the api may support this now)
- This solution clears everything, then writes back everything EXCEPT the deleted setting - this was required, in the past. 

---

## Visual Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        USER ACTION                              │
└─────────────────────────────────────────────────────────────────┘
                                │
        ┌───────────────────────┼───────────────────────┐
        ▼                       ▼                       ▼
   [UPDATE/ADD]            [DELETE]                [READ]
        │                       │                       │
        ▼                       ▼                       ▼
   Clone setting (in js)    Confirm x2           GET /organizations
        │                       │                       │
        ▼                       │                       ▼
   Validate value               │              Parse orgdborgsettings
        │                       │                  XML field
        ▼                       ▼
   Serialize to XML        PATCH #1: Clear
<Setting>val</Setting>   { orgdborgsettings:  "" }
        │                       │
        ▼                       ▼
   PATCH request          Rebuild XML without
   {orgdborgsettings:      deleted setting
     "<orgSettings>..."}        │
        │                       ▼
        │                 PATCH #2: Write back
        │                 { orgdborgsettings:  "..." }
        ▼                       ▼
   ┌─────────────────────────────────────────────────────────────┐
   │                    UPDATE UI & DISPLAY                      │
   └─────────────────────────────────────────────────────────────┘
```

---

## Key Takeaways

| # | Point |
|---|-------|
| 1 | **API** - Just one endpoint with PATCH for all mutations |
| 2 | **XML Blob Storage** - All OrgDbOrgSettings are stored as XML in a single field |
| 3 | **Delete = Reconstruct** - Deleting requires clearing and rebuilding the entire settings blob |
| 4 | **Dual Paths** - OrgDbOrgSettings go to the XML blob in the organization.orgdborgsetting attribute; Any Organization Attributes listed can update organization entity columns directly |

---

## Source Repository

This analysis is based on the code from:  [seanmcne/OrgDbOrgSettings](https://github.com/seanmcne/OrgDbOrgSettings)

Primary source file: `orgDBOrgSettings.html`
