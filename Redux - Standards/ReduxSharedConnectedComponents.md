# Redux - Shared Connected Components

A Shared Connected Component is a component that is only connected to a private Slice and/or to one or more Shared Slices.

Think of a Shared Connected Components as configurable organisms. 
The external props of a Shared Connected Component allow the consumer to configure it.
All necessary logic and state is self contained into its private Slice and/or other Shared Slices that the component is using. 

Packaging the Connected Component into a NPM library allows the reuse of that Connected Component in multiple Redux applications.

## Redux Libraries 

The following Redux libraries have been created to host Shared Connected Components and Shared Slices:

* [DealerSocket.Redux.Common](https://bitbucket.org/dealersocket/dealersocket.redux.common/src/master/)
Shared Slices and Shared Connected Components that are not Tribe specific
 
* [DealerSocket.Redux.Crm](https://bitbucket.org/dealersocket/dealersocket.redux.crm/src/master/)
CRM Tribe specific Shared Slices and Shared Connected Components

* [DealerSocket.Redux.Inventory]()
Inventory Tribe specific Shared Slices and Shared Connected Components


## How to share a Connected Component
todo


## How to use a shared Connected Component
todo