# Custom fields

Send custom field values when you create or update records through the SmartHive Projects APIs.

Custom fields are configured in module layouts to capture additional information based on business needs. To pass values in the request payload, use the API names of the corresponding fields.

For example, you can use a checkbox custom field to track a project condition and submit its value as true or false in the API request.

**Note:***

- Custom field API names are currently supported only in the Tasks and Projects APIs.
- Before you pass values, use the Custom Fields metadata API to get field details such as API names and field types.