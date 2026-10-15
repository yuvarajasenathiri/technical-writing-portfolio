# API names

Understand, locate, and use API names for modules, fields, and related APIs in SmartHive Projects.

SmartHive Projects assigns a unique identifier, called an API name, to every module and field.

Display names, the labels shown in the UI, can change and can include spaces or special characters. API names stay the same across API requests and responses, so they give you a consistent reference.

### Display name vs. API name

| Aspect	| Display name |	API name |
| :---        | :----  |      :---- |
| Purpose	| A label shown in the UI |	An identifier used in APIs |
| Example	 | Start Date	| `start_date` |
| Stability |	Can change	| Stays constant |
| Used in	| Forms, views, and layouts |	Requests, responses, and filters|

## Usage

You use API names in all programmatic interactions with SmartHive Projects.

### Requests and responses

API names appear as keys in request payloads and response data. You reference fields such as priority, status, and department by their API names, not their display labels. This applies to operations such as 
creating, updating, retrieving, and filtering records.

## Retrieve API names

You can find API names for modules and fields in SmartHive Projects in the product or by using the APIs.

### Method 1: Use the product

The **Fields** section in SmartHive Projects shows the API names for custom fields next to other field details.

1. Select **Setup** > **Customization** > **Fields**.
2. Select the module you need.
3. Use **Search** Fields to find a specific field in the Fields list.
4. Copy the API name to use in API operations.

### Method 2: Use the APIs

The Modules API returns metadata for all modules in a portal, including their API names. The Fields API returns metadata for all fields in a module, including API names, data types, and whether each field 
is custom. Together, they give you a complete reference of the available modules and fields.

- For the list of modules and their API names, see Get Modules.
- For field-level details, including API names, see Get Fields Info.