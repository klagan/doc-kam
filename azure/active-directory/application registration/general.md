# General

### App Registrations
This is where you reserve the URL and associated IDs allowing your application to communicate with Azure AD.
#azure

### Enterprise Applications
This is where you manage the access and integration for *all* applications with your Azure tenant.  
This includes third party applications like Office 365 and Facebook and home grown applications.
#azure

> https://stackoverflow.com/questions/54071385/difference-between-enterprise-application-and-app-registration-in-azure

### Role based access control (RBAC)

> https://docs.microsoft.com/en-gb/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps

> https://github.com/Azure-Samples/active-directory-aspnetcore-webapp-openidconnect-v2/tree/master/5-WebApp-AuthZ/5-1-Roles#choose-the-azure-ad-tenant-where-you-want-to-create-your-applications

1. Register Application
2. Create application roles in the manifest (application/user)

**Permissions** - `delegated` and `application`.  
`Delegated` permissions are where a user is signed in.  The applications will act *on behalf of* the signed in user.
`Application` permissions are where there is no signed in user.  eg: daemon or service.

**Scopes** - application defines things it requires the consent of the user eg: read user data from a service, write user data to a service.  These are considered user permissions for user owned data or services.

**Roles** - these are defined by the administrator of the application.  The application will use roles to control what the user can and can't do eg: The application may write data if the user is a member of the `writer` role.

`Roles` allow the user to do something
`Scopes` allow the application to do things on behalf of the user/application.

### Quick summary
Web Applications
- allows a user to log into the web app by getting an id token
- make call to web api
- check cache - if fail then throw exception that the code expects to be caught in the `AcquireForScopes` attribute
- this attribute will set a few things before retrying
- once the access token is retrieved - using the id token) - it is cached (in memory for the example)
- the access token is then embedded as an authorisation header in the http request made through the http client

Web API
- `startup.cs` sets up all the expectations on the authorisation and tokens
- controller is protected by `Authorise` and `AuthorizeForScopes` attributes

Remember to apply security to the web api.  It is the resource that needs primary protection against the world.  The consumer can also have security applied but as a secondary layer.  The resource is responsible for protecting itself.

# Add application/user roles to an application manifest

Add a section similar to this making sure that the GUID is unique to the section block:

```
"appRoles": [
		{
			"allowedMemberTypes": [
				"User"
			],
			"description": "Administrators",
			"displayName": "MyAdmin",
			"id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
			"isEnabled": true,
			"value": "MyAdmin"
		},
		{
			"allowedMemberTypes": [
				"User", "Application"
			],
			"description": "Noddy users",
			"displayName": "Noddy User",
			"id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
			"isEnabled": true,
			"value": "NoddyUser"
		}
	],
```

---

# Authentication

> *AT* - access token
> *RT* - refresh token

Client is registered with authorisation server

A *confidential client* is a client that is capable of maintaining credentials and/or obtaining client authentication securely.  

A public client is one that is not a *confidential client*.

A *resource owner* is an entity that provides credentials to access a protected resource.
Both a client and an end user entity could be a resource owners.


**Implicit grant**
Public client - eg: SPA
The end user entity is the resource owner
Client is **not** authenticated
Authorisation returns access token
Access token is available through the front channel
*AT* 

**Client credential grant**
Client is the resource owner
Machine to machine authentication
There is no end user entity

*AT*

**Resource owner password credential grant**
End user entity is the resource owner but the client has access to the resource owners user credential
Used when the client and authorisation server are trusted and/or developed by the same organisation
*RT* *AT*

**Authorisation code grant**
Makes use of back channels for minimum exposure of tokens
Returns an authorisation token which must be exchanged at the token endpoint

**Hybrid grant**
May be returned the authorisation code and either the id token or authorisation token or both