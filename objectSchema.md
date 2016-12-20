# Core Object Types

## MinimalDSO
* uuid: uuid
* name: String
  * name will be pre-loaded from metadata 
* type: enum of DSO
* handle: String
* url() : String 
* accessible: enum of accessibility summary (for current user)
* toDSO(): DSO

## DSO extends MinimalDSO
* policies(): Array of Policy
* metadata(): Array of Metadata

## HierarchicalDSO extends DSO
* breadcrumb: Array of MinimalDSO
* descendants: Hierarchy

## Repository extends HierarchicalDSO

## Community extends HierarchicalDSO

## Collection extends HierarchicalDSO
* items: Array of Items
* contentSource: enum

## Item extends DSO
* breadcrumb: Array of MinimalDSO
* bitstreams: Array of Bitstream
* submitter: EPerson
* discoverable: boolean
* withdrawn: boolean
* in_archive: boolean

## Bundle 
* Can we abstract this out so REST client does not directly manipulate this?

## Bitstream extends DSO
* parentItem: Item
* bundleName: String
* sequence: Number
* formatId: Number or enum
* checksum: String
* checksumAlgorithm: enum
* deleted: boolean
* size: Number
* internal id - should this be exposed externally?
* associatedItems: Array of Object
  .bundleName
  .bitstream

## Metadata
* dspaceObject: UUID
* schema: String
* element: String
* qualifier: String
* key: String (schema+element+qualifier)
* text_value: String
* lang: String or enum
* sequence: Number
* authority: String
* confidence: Number

## Policy - DSpace access policy info
* dspaceObject 

# Brainstorm Object Types

## SolrMetadata
* field: String
* value: String
* hit: String representation of values with search hits embedded

## SearchResult
* dso: MinimalDSO
* metadata: Array of SolrMetadata 
* snippet: Array of SolrMetadata

## NodeContext
* breadcrumb: array of MinimalDSO
* descendants: Hierarchy
* browseOptions: Array of Option
* browseFacets: Array of Facet
* actions: Array of Actions
* searchResults: Array of SearchResult

## Hierarchy
* node: MinimalDSO (repo, community, collection)  
* children: Array of Hierarchy 

## Property
* module - String
* name - String
* dataType - Number, String, Array, Date, Map
* value - Object

## Option
* name - nmtoken string to be passed as a URL
* desecription - String describing the option

## Facet
* facetName - String
* facetType - Value sorted, alpha sorted
* moreUrl - Url to retrieve more values
* facetValues - Array
  * valueName - String
  * valueCount - Number
  * url - url for facet?

## Action
* name - String - action name
* actionType - enum categorizing action behavior
* url - Url to invoke action

* Examples
  * Admin Action (Create, Edit, Export)
  * Workflow Action (Submit)
  * Aux Action (Usage stats)
