# Core Object Types
## DSO
* uuid: uuid
* name: String
* type: enum of DSO
* handle: String
* accessible: enum of accessibility summary (for current user)

## Repository extends DSO

## Community extends DSO
* breadcrumb: Array of DSO
* metadata: Array of Metadata
* hierarchy: Hierarchy
* policies: Array of Policy

## Collection extends DSO
* breadcrumb: Array of DSO
* metadata: Array of Metadata
* policies: Array of Policy
* items: Array of Items
* contentSource

## Item extends DSO
* breadcrumb: Array of DSO
* metadata: Array of Metadata
* policies: Array of Policy
* bitstreams: Array of Bitstream

## Bundle 
* Can we abstract this out so REST client does not directly manipulate this?

## Bitstream 
* parentItem: Item
* bundleName
* sequence
* associatedItems: Array of Object
  .bundleName
  .bitstream

## Metadata
* schema
* element
* qualifier
* value
* sequence
* authority

## Policy - DSpace access policy info


# Brainstorm Object Types

# Browse
* breadcrumb: array of DSO
* descendants: Hierarchy
* metadata: Array of Metadata
* browseOptions: Array of Option
* browseFacets: Array of Facet
* browseItems: Array of Item
* actions: Array of Actions

# Hierarchy
* node: DSO (repo, community, collection)  
* children: Array of Hierarchy 

# Property
* module - String
* name - String
* dataType - Number, String, Array, Date, Map
* value - Object

# Option
* name - nmtoken string to be passed as a URL
* desecription - String describing the option

# Facet
* facetName - String
* facetType - Value sorted, alpha sorted
* moreUrl - Url to retrieve more values
* facetValues - Array
  * valueName - String
  * valueCount - Number
  * url - url for facet?

# Action
* name - String - action name
* actionType - enum categorizing action behavior
* url - Url to invoke action

* Examples
  * Admin Action (Create, Edit, Export)
  * Workflow Action (Submit)
  * Aux Action (Usage stats)
