# Core Object Types

## MinimalDSO
* uuid: uuid
* name: String
  * name will be pre-loaded from metadata 
* type: enum of DSO
* handle: String
* url() : String 
* accessible: enum of accessibility summary (for current user)
* toDSO(): [DSO](#dso)

## DSO 
* extends [MinimalDSO](#minimaldso)
* policies(): Array of [Policy](#policy)
* metadata(): Array of [Metadata](#metadata)

## HierarchicalDSO 
* extends DSO
* breadcrumb: Array of [MinimalDSO](#minimaldso)
* descendants: [Hierarchy](#hierarchy)

## Repository 
* extends [HierarchicalDSO](#hierarchicaldso)

## Community 
* extends [HierarchicalDSO](#hierarchicaldso)

## Collection 
* extends [HierarchicalDSO](#hierarchicaldso)
* items: Array of Items
* contentSource: enum

## Item 
* extends [DSO](#dso)
* breadcrumb: Array of [MinimalDSO](#minimaldso)
* bitstreams: Array of [Bitstream](#bitstream)
* submitter: [EPerson](#eperson)
* discoverable: boolean
* withdrawn: boolean
* in_archive: boolean

## Bundle 
* Can we abstract this out so REST client does not directly manipulate this?

## Bitstream 
* extends [DSO](#dso)
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
  
## EPerson
* extends [DSO](#dso)

## EPersonGroup
* extends [DSO](#dso)

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

## Policy 
* dspaceObject: [DSO](#dso)
* personOrGroup: [DSO](#dso)
* action: enum

# Brainstorm Object Types

## SolrMetadata
* field: String
* value: String
* hit: String representation of values with search hits embedded

## SearchResult
* dso: [MinimalDSO](#minimaldso)
* metadata: Array of [SolrMetadata](#solrmetadata) 
* snippet: Array of [SolrMetadata](#solrmetadata)

## NodeContext
* breadcrumb: array of [MinimalDSO](#minimaldso)
* descendants: [Hierarchy](#hierarchy)
* browseOptions: Array of [Option](#option)
* browseFacets: Array of [Facet](#facet)
* actions: Array of [Action](#action)
* searchResults: Array of [SearchResult](#searchresult)

## Hierarchy
* node: [MinimalDSO](#minimaldso) (repo, community, collection)  
* children: Array of [Hierarchy](#hierarchy) 

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
  
## CurationSpec
* Task Name
* Scope Node: Repo / Community / Collection uuid
* Task Parameters

## CurationResult
* CurationSpec
* CurationOuput