# OAuth scope

Scope limits the level of access the application can have when making requests to the resource server (to access protected resources). It is what enables the user to provide delegated access to the client.



For example, if the client only needs to access the Asset Master module in SmartHive, then it can be defined in the scope when requesting for access token. When the client makes API requests with the access 
token, the resource server will provide access only to the Asset Master module. It can also be defined what kind of operations (create/read/update/delete) are permissible for the client with respect to the module.

**Syntax:** `service_name.scope_name.OPERATION_TYPE`

**Example:**

- `SmartHiveAssetMaster.users.CREATE`
- `SmartHiveProduct.configure.UPDATE`

When the user is asked for permission to grant access to the client, the scopes defined in the request will be shown.

A SmartHive OAuth scope has three parts:

- **Service name:** The name of the service the client is making API calls to. All SmartHive modules have a unique service name such as SmartHiveassetmaster, or SmartHiveproduct.
- **Scope name:** The name of the module in the service the client needs access to. Each SmartHive service is divided into different modules. You can view the scope names from the respective module's API docs.
- **Operation type:**  The type of operation that is permissible for the client. It can be `ALL`, `READ`, `UPDATE`, `DELETE`. (`ALL` gives access to perform all operations).

**Note**

Access tokens can also be generated with multiple scopes. In such cases, the scopes should be separated by commas.

- **SYNTAX:** `service_name.scope_name.OPERATION_TYPE,service_name.scope_name.OPERATION_TYPE` 

- **Example:** `SmartHiveAssetMaster.users.CREATE,SmartHiveProduct.configure.UPDATE`