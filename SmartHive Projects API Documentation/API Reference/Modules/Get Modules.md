# Get modules

Use this endpoint:

- To retrieve a list of modules in the portal, along with their configuration details. 
- To identify module API names, IDs, and types before you perform module-level operations.

**Method and endpoint:** `GET /api/v3/portal/[PORTAL_ID]/settings/modules`

**OAuth scope:** *SmartHiveProjects.custom_fields.READ*

**Path parameters**
| Name |	Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `portal_id` |	String<br>digits only ([0-9]+ 	| Required | The unique, immutable identifier of the portal in SmartHive Projects.<br>Get it from the [Get All Portals with Details API](#get-all-portals-with-details-API) (the `id` field in the response).|

**Request example**
```
curl -X GET \
 'https://projects.smarthive.com/api/v3/portal/[PORTAL_ID]/settings/modules?filter=%7B%22is_customized%22%3Atrue%2C%22is_default%22%3Atrue%2C%22is_web_tab%22%3Atrue%7D&page=1&per_page=10' \
 -H 'Authorization: Bearer 1000.03xxxxxxxxxxxxxxxxxa5317.dxxxxxxxxxxxxxxxxxfa'
```
**Query parameters**

> In the following table, a dot in a name shows that the parameter is a property of the object before it, and [] shows an array item.

|Name	| Data type | Required/Optional |	Description |
| :---        | :----  |   :----  |   :---- |
| `filter`	| JSONObject | Optional |	The filter criteria for refining the results.<br> You can combine multiple filter conditions. |
| &emsp; filter.is_`customized` |	Boolean |	| Whether to include only customized modules. |
| &emsp; filter.is_`default`	| Boolean	| | Whether to include only default modules.|
| &emsp; filter.`is_web_tab` | 	Boolean | |Whether to include only web tab modules.| 
| `page` |	Integer<br>*Default: 1* |	|The page number.|
| `per_page` |	Integer<br> *Limit: 1 to 200*<br>*Default: 1,000*| 	| The number of entries to display on each page.|

**Sample input**
```
filter : {
  "is_customized" : true,
  "is_default" : true,
  "is_web_tab" : true
}
page : "1"
per_page : "10"
```
**Sample response**
- 200 Ok
```
[ {
  "id" : "4000000000152",
  "api_name" : "tasks",
  "singular_name" : "Task",
  "icon_class" : "zoho-task",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Task",
  "module_name" : "Task",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "5",
    "is_indexed_module" : true,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000000155",
  "api_name" : "issues",
  "singular_name" : "zp.general.issue",
  "plural_name" : "zp.general.issues",
  "icon_class" : "zoho-bugs2",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Issue",
  "module_name" : "Issue",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "6",
    "is_indexed_module" : true,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000000158",
  "api_name" : "timelogs",
  "singular_name" : "zp.tab.timelog",
  "plural_name" : "zp.tab.timelogs",
  "icon_class" : "zoho-timesheet",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Timesheet",
  "module_name" : "Timesheet",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000000521",
  "api_name" : "projects",
  "singular_name" : "Projects",
  "icon_class" : "zoho-projects",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Projects",
  "module_name" : "Projects",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "2",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000000776",
  "api_name" : "phases",
  "singular_name" : "zp.module.rename.phase",
  "plural_name" : "zp.module.rename.phases",
  "icon_class" : "zoho-milestone",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Milestone",
  "module_name" : "Milestone",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "3",
    "is_indexed_module" : true,
    "default_layout_type" : "private"
  }
}, {
  "id" : "4000000002061",
  "api_name" : "tasklists",
  "singular_name" : "zp.module.tasklist",
  "plural_name" : "zp.module.tasklists",
  "icon_class" : "zoho-tasklist",
  "type" : "default",
  "status" : "active",
  "is_global_module" : false,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Tasklist",
  "module_name" : "Tasklist",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "4",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002064",
  "api_name" : "forums",
  "singular_name" : "zp.forum.tab",
  "plural_name" : "zp.profileform.forum",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Forum",
  "module_name" : "Forum",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "7",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002067",
  "api_name" : "statuses",
  "singular_name" : "zp.reports.status",
  "plural_name" : "zp.customfields.statuses",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Status",
  "module_name" : "Status",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "8",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002070",
  "api_name" : "events",
  "singular_name" : "zp.notification.event",
  "plural_name" : "zp.todo.events",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Events",
  "module_name" : "Events",
  "is_overview_needed" : true,
  "module_property" : {
    "search_module_id" : "9",
    "is_indexed_module" : true,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002073",
  "api_name" : "pages",
  "singular_name" : "zp.planacc.wikis",
  "plural_name" : "zp.planacc.wikis",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Pages",
  "module_name" : "Pages",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002076",
  "api_name" : "documents",
  "singular_name" : "zp.doc.tab",
  "plural_name" : "zp.doc.tab",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Documents",
  "module_name" : "Documents",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002079",
  "api_name" : "users",
  "singular_name" : "zp.general.user",
  "plural_name" : "zp.general.users",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Users",
  "module_name" : "Users",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002082",
  "api_name" : "clients",
  "singular_name" : "zp.client.clientcompuser",
  "plural_name" : "zp.planaccount.clients",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Clients",
  "module_name" : "Clients",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002085",
  "api_name" : "resources",
  "singular_name" : "zp.resources.resource",
  "plural_name" : "zp.tasklistexport.resource",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Resources",
  "module_name" : "Resources",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002088",
  "api_name" : "timeloggroup",
  "singular_name" : "zp.tsheet.tab",
  "plural_name" : "zp.invoice.timesheets",
  "icon_class" : "zoho-timesheet-new",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "TimelogGroup",
  "module_name" : "TimelogGroup",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002091",
  "api_name" : "recyclebin",
  "singular_name" : "zp.module.recyclebin",
  "plural_name" : "zp.module.recyclebin",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Recyclebin",
  "module_name" : "Recyclebin",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000002094",
  "api_name" : "customers",
  "singular_name" : "zp.client.clientcompname",
  "plural_name" : "zp.client.companies",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : false,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Customers",
  "module_name" : "Customers",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000060007",
  "api_name" : "tags",
  "singular_name" : "zp.links.tag",
  "plural_name" : "zp.tag.tags1",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Tag",
  "module_name" : "Tag",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000060016",
  "api_name" : "profiles",
  "singular_name" : "zp.userfilter.profile",
  "plural_name" : "zp.settings.profiles",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Profile",
  "module_name" : "Profile",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
}, {
  "id" : "4000000060025",
  "api_name" : "roles",
  "singular_name" : "zp.userfilter.role",
  "plural_name" : "zp.settings.roles",
  "icon_class" : "zoho-ext-icon1",
  "type" : "default",
  "status" : "active",
  "is_global_module" : true,
  "is_all_projects" : true,
  "is_all_profiles" : true,
  "overviewNeeded" : true,
  "tabName" : "Role",
  "module_name" : "Role",
  "is_overview_needed" : true,
  "module_property" : {
    "is_indexed_module" : false,
    "default_layout_type" : "public"
  }
} ]
```