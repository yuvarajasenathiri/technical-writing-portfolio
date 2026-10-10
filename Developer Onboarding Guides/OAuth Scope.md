# OAuth scope

A scope limits the level of access that an app has when it makes requests to the resource server to access protected resources. Scopes enable the user to give the client delegated access.

For example, if the client needs to access only the Asset Master module in SmartHive, you can define that in the scope when you request an access token. When the client makes API requests with the access token, 
the resource server provides access only to the Asset Master module. You can also define which operations (create, read, update, or delete) the client can perform on the module.

**Syntax:** `service_name.scope_name.OPERATION_TYPE`

**Example:**

- `SmartHiveAssetMaster.users.CREATE`
- `SmartHiveProduct.configure.UPDATE`

When SmartHive asks the user to grant access to the client, it shows the scopes defined in the request.

A SmartHive OAuth scope has three parts:

- **Service name:** The name of the service that the client makes API calls to. Every SmartHive module has a unique service name, such as SmartHiveAssetMaster or SmartHiveProduct.
- **Scope name:** The name of the module in the service that the client needs to access. Each SmartHive service is divided into modules. To find scope names, see the API documentation for the module. 
- **Operation type:**  The type of operation that the client can perform: `ALL`, `READ`, `UPDATE`, `DELETE`. `ALL` gives access to  all operations.

**Note**

You can generate an access token with multiple scopes. Separate the scopes with commas.

- **SYNTAX:** `service_name.scope_name.OPERATION_TYPE,service_name.scope_name.OPERATION_TYPE` 

- **Example:** `SmartHiveAssetMaster.users.CREATE,SmartHiveProduct.configure.UPDATE`