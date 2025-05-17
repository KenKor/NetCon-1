---
title: Version Information
description: 
permalink: 
aliases: 
draft: false
date: 2025-05-16
Version: 2024.1.3
Product: NetCon 2.0
tags:
  - ToDo
---
[[../1 Introduction/Introduction|previous]] [[./Roadmap||next]]
# Releases

This paragraph contains the version information for the `Spatial Eye NetCon` product(s). The product's change history is described below for each of the released versions.

|              Version               | Released    |
| :--------------------------------: | ----------- |
| [[Version Information#Spatial Eye NetCon 2024.1.3.8|Spatial Eye NetCon 2024.1.3.8]] | 16 mei 2025 |
| [[Version Information#Spatial Eye NetCon 2024.1.3.7|Spatial Eye NetCon 2024.1.3.7]] | 17 apr 2025 |
| [[Version Information#Spatial Eye NetCon 2024.1.3.6|Spatial Eye NetCon 2024.1.3.6]] | 10 apr 2025 |
| [[Version Information#Spatial Eye NetCon 2024.1.3.5|Spatial Eye NetCon 2024.1.3.5]] | 25 mar 2025 |
| [[Version Information#Spatial Eye NetCon 2024.1.3.4|Spatial Eye NetCon 2024.1.3.4]] | 18 feb 2025 |
| [[Version Information#Spatial Eye NetCon 2024.1.3.3|Spatial Eye NetCon 2024.1.3.3]] | 6 feb 2025  |
| [[Version Information#Spatial Eye NetCon 2024.1.3.2|Spatial Eye NetCon 2024.1.3.2]] | 5 feb 2025  |
| [[Version Information#Spatial Eye NetCon 2024.1.3.1|Spatial Eye NetCon 2024.1.3.1]] | 17 jan 2025 |
| [[Version Information#Spatial Eye NetCon 2024.1.3.0|Spatial Eye NetCon 2024.1.3.0]] | okt 2024    |
| [[Version Information#Spatial Eye NetCon 2023.4.1.0|Spatial Eye NetCon 2023.4.1.0]] | mar 2024    |
| [[Version Information#Spatial Eye NetCon 2023.3.3.0|Spatial Eye NetCon 2023.3.3.0]] | nov 2023    |
| [[Version Information#Spatial Eye NetCon 2023.1.1.0|Spatial Eye NetCon 2023.1.1.0]] | mar 2023    |
| [[Version Information#Spatial Eye NetCon 2022.4.0.0|Spatial Eye NetCon 2022.4.0.0]] | dec 2022    |

# Release Notes


---
## Spatial Eye NetCon 2024.1.3.8

In a future release: the location of the documentation will change to:
	https://spatial-eye.github.io/NetCon/

Fixes:
* When an invalid search predicate was provided, this would result in an error, even though the [[../7 NetConQL/NetConQL - Network Connection Query Language|NetConQL - Network Connection Query Language]] parser would ignore the error, as can be seen in the query recipe that is returned and logged. As a result of this fix, an invalid predicate will return false.
* Empty values provided by the extraction process in AssetHierarchy and Specification, will return `null` values instead of `NaN` (previously used as an error value). So, a NetConConnection record with AssetHierarchy ::= "SubStation.Id=" will now return `null` when the Id of the SubStation is queried.
* (Testing not finished.) In exceptional cases, the TraceAPI does not produce any output. This depends on the input data. The TraceAPI needs to be hardened.
* Queries of Type : SELECT * FROM TRACE(... START Id=123,456) where incorrectly translated to SELECT * FROM TRACE(... START Id LIKE 123,456) but will not be translated to SELECT * FROM TRACE(... START Id LIKE [123,456]) and corresponding list processing.

Changes:
* When the TraceAPI writes results, the precious of doubles has been increased by two digits.
* When the TraceAPI writes results, the AssetId property is of type long. It used to be written as a string.
* Performance improvements during various traces and data loading. Speed of comparing of Connections and Paths internally has been increased.
* Analogue to [[../8 API/Calls/GetOperatedSection|GetOperatedSection]], [[../8 API/Calls/GetControlSection|GetControlSection]] and [[../8 API/Calls/GetCustomSection|GetCustomSection]] have been added as [[../8 API/NetCon API Calls|NetCon API Calls]].
* The [[../8 API/Calls/Statistics|Statistics]] API is separated from the [[../8 API/Calls/DataQuality|DataQuality]] API.
* The [[../8 API/Calls/Statistics|Statistics]] API is extended with some more analyses, including a property that can be provided by the caller.
* The [[../8 API/Calls/Catalogs|Catalogs]] API has been implemented.
* [[../6 Use/Enumerators/NetCon EdgeType Enumerator|NetCon EdgeType Enumerator]] loop has been renamed to self-loop, since only loop going to and from the same node id are intended.

---
## Spatial Eye NetCon 2024.1.3.7

Fixes:
* When NetCon trace expressions such as [[../8 API/Calls/TracePathUpstream|TracePathUpstream]] or [[../9 Expressions/NetworkResult Expressions/TraceOut()|TraceOut()]] where invoked subsequent expressions such as First() or Last(), to get e.g. the AssetId of the first upstream transformer or low side bus, would produce an error if no results are found. The software is now resilient to this.

---
## Spatial Eye NetCon 2024.1.3.6

Fixes:
* When generating [[../5 Configuration/Sectioning and Tracing/Sections/Control or NetCongestion Section|Control or NetCongestion Section]], when the same AssetTableName is used the barrier control sections (e.g. main switches feeding a downstream part of the network) and also occurs in the non-barrier control section that is fed from it, the predicate to find a busbar or rail upstream could fail. The software is now resilient to this.

---
## Spatial Eye NetCon 2024.1.3.5

Changes:
* In [[../8 API/Results/Connection Or Path Results/AssetHierarchy|AssetHierarchy]] and [[../8 API/Results/Connection Or Path Results/Specification|Specification]], it is possible to use quotes.
* It is now possible to create [[../5 Configuration/Properties/Property Type Definition|Property Type Definition]], to force a type when properties are is parsed from a string (e.g. during querying or as used in AssetHierarchy or Specification.
* [[../5 Configuration/Overlay and Near Real Time Networks/Introduction to Overlay Networks|Overlay networks]] are made available.
* [[../6 Use/Enumerators/NetCon EdgeType Enumerator|NetCon EdgeType Enumerator]] node has been renamed to loop, since and edge is never a node, but a 'loop' was intended.

---
## Spatial Eye NetCon 2024.1.3.4

Fixes:
* In the TraceAPI, the [[../8 API/Parameters/ExpandPaths|ExpandPaths]] parameter is ignored. Note that the default of [[../8 API/Parameters/ExpandPaths|ExpandPaths]] may have changed, see the link. 
* The Start and Stop predicates like `Commodity->Net=LS` would not take into account multiple parameters. They are now rewritten as `Commodity->(Net=LS)` so `Commodity->(Net=LS AND Function>=10000)` will work.
* The [[../8 API/Parameters/SmartStart|SmartStart]] parameter has been improved that it will also work when no start criteria have been provided (in which case the trace defaults will be set - see the individual trace functions).

Changes:
* The internal start up procedures have been changed to allow for Overlay Networks. An overlay network can be used for Data Quality or Data Patching purposes and will create a new network that depends on another one. In queries, you can specify the Network to be queries with the [[../9 Expressions/Parameters/NetworkName|NetworkName]] parameter.
* A new parameter [[../8 API/Parameters/StopAtBarringConnections|StopAtBarringConnections]] has been added to [[../8 API/Calls/TraceOut|TraceOut]] and [[../8 API/Calls/TraceMazed|TraceMazed]]. It needs to be researched if this makes sense when Flow is used, since there is propably no flow at barring barriers. The [[../8 API/Parameters/BlockBarringConnections|BlockBarringConnections]] is ignored if the new parameter is set since it would undo the other one.
* When reporting all data quality problems for large networks, the [[../8 API/Calls/Statistics|Statistics]] API is too slow to produce an answer within the time limit. As a result `504 gateway timeout` is received. The default parameter is changed to skip data quality checks.

---
## Spatial Eye NetCon 2024.1.3.3

Fixes:
* When [[../8 API/Parameters/BlockBarringConnections|BlockBarringConnections]] was set in combination with other block criteria, it would use AND rather than OR logic. This has been corrected.

---
## Spatial Eye NetCon 2024.1.3.2

Fixes:
* In the JSon results of the API, the AssetHierachy part was empty. 
* In the JSon results of the API, owner and operated-by properties were not filled out correctly.
* Specifying Start, Block, Yield and Block criteria for AssetHierachy, Commodity, and Specification required a prefix with this name and "->". This has been removed. So now, one can use "e_stationcomplex->id=211712133" or e_stationcomplex->name="Vos", for example.
* In the API, the MaxResults parameter was ignored.

---
## Spatial Eye NetCon 2024.1.3.1

Deployment:
* Make sure on the [[Network Trace Feature Source|Network Trace Feature Source]] to specify the generation of indices (if you are querying a large network).

New:
* Support for generating Control sections.
* Parameters of the API calls have been renamed.
* Trace API calls now produce queries, that communicate back their recipe in the results.
* Trace API calls with Commodity, AssetHierarchy, and Specification now support complex querying, using AND, OR, NOT, LIKE, IN, >=, >, etc. See [[../7 NetConQL/NetConQL - Specification|NetConQL - Specification]].
* #ToDo Complete this list.

Changes:
* The GeoJSon result for Commodity, AssetHierarchy, and Specification is expanded into sub properties.
* Underlying indices generation has changed. In principle, it is possible to have an index only any start condition that you use often. Let us know if custom or extra indices are required to speed up the initial search.
* FeederSection was renamed to ControlSection. Additional CustomSection are enabled, to offer freely configurable sectioning.
* #ToDo Complete this list.

---
## Spatial Eye NetCon 2024.1.3.0

New:
* Support for API-call [[../8 API/Calls/TraceOutageImpact|TraceOutageImpact]].

---
## Spatial Eye NetCon 2023.4.1.0

New:
- [[Flow calculation|Flow calculation]] is added and computed on the fly to determine the direction of the flow (none, down or mazed) for every connection. If not start criterion is specified, the [[../3 Overview/Sources|source]] is used.
- [[Flow calculation export|Flow calculation export]] is enabled for various network flow calculation programs.
- [[NetCon sections|NetCon sections]] are computed on the fly. This allows for a faster startup. Sections are name Isolatable, Operated, Control and Custom sections. The sections have now more attributes than the previous Section and Super sections. The relations between sections and connections have been simplified.
	- The sections themselves are not only available as feature source tables so they can be materialized (see [[../6 Use/Long running queries/Materializing Long Running traces|Materializing Long Running traces]]), but also their traces are available to be persisted.
- [[../5 Configuration/Enrichment/Specification Enrichment|Specification enrichment]], [[../5 Configuration/Enrichment/Asset Hierarchy Enrichment|Asset Hierarchy Enrichment]] and [[../5 Configuration/Enrichment/Asset Enrichment|Asset Enrichment]] have been added to enable central enrichment of connectivity information. This way, the entire organisation can benefit from a single source of truth.
- Over 300 units tests have been programmed that are run as part of the release process.

Updated:
* The tracing algorithms have been rewritten to inherit from the same abstract class. They are all operating in a streamed fashion.
* The new operated sections do not have the option to 'copy' cutting sections with transformer or switch to the adjacent neighbours. This helps keeping the relationship clearer, but is incompatible with the previous release. Therefore, the previous sectioning (aggregator DLL) is still supported, so dependent applications can be ported.
- [[../9 Expressions/NetCon Expressions|NetCon Expressions]] have been added and rewritten.
- [[../8 API/NetCon API Calls|NetCon API]] have been adapted. It has been made streamed where possible. Because of this the output objects has a different field order.
- The trace [[../8 API/NetCon API Calls|NetCon API]] calls have been updated to have more [[../8 API/Parameters/ExpandPaths|ExpandPaths]] options.

Changes per release 29 Oct 2024
* The parameter [[../8 API/Parameters/ExpandPaths|ExpandPaths]] has new default values and is now passed as a string, no longer as an integer value.
* The parameter `patternIsRegex` has been renamed [[PatternIsRegex|PatternIsRegex]] for all functions.
* The parameter [[../8 API/Parameters/CommodityPattern|CommodityPattern]] has been added to all search en trace function. At this moment, only [[CommodityNet|CommodityNet]] will be filtered. Please note that not every connection has a Commodity set (see enhancement below).
* The parameter [[../8 API/Results/Connection Or Path Results/AssetId|AssetId]] is not longer overloaded; a new parameter [[../8 API/Parameters/ConnectionIds|ConnectionIds]] has been added when the id of a connection is intended.
* The result attribute [[../8 API/Results/Connection Or Path Results/Specification|Specification]] takes special precaution when its property keys is called `id`.
* Fixed: The start or search parameters do not work correctly when no [[../8 API/Parameters/AssetTableNamePattern|AssetTableNamePattern]] is provided.
* Fixed: The results count for expanded paths is corrected. In the previous release it pointed to the number of paths matching the 'yield' predicate instead of the number of returned items.

Changes per release 30 Oct 2024
* Fixed: The parameters [[../8 API/Parameters/CommodityPattern|CommodityPattern]] and [[../8 API/Parameters/AssetTableNamePattern|AssetTableNamePattern]] would cause an error if there is only one matching result.

Changes per release 31 Oct 2024
* The predicates in [[../5 Configuration/Sectioning and Tracing/NetConTrace feature source|NetConTrace feature source]] can now take on many more and different arguments. Previously they only accepted assettablesnames like `assettablenames=*somepattern,another`.
* The result attribute `flag` has been renamed to [[../8 API/Calls/TraceMazed|TraceMazed]]. This affects all results.

Enhancement requests:
* When a NetConConnection has no [[../3 Overview/Commodity|Commodity]], derive it from its upstream neighbors.

---
## Spatial Eye NetCon 2023.3.3.0

New:
- [[../9 Expressions/NetCon Expressions|NetCon Expressions]] to compute traces and query in all the Spatial Eye products.
- [[../8 API/NetCon API Calls|NetCon API]] has been made available for the Spatial Eye server product.
- [[../8 API/Results/Connection Or Path Results/Label|Label]] property has been added to the Connection definition to allow for a company wide name ontology.
- [[../8 API/Parameters/SpecificationPattern|SpecificationPattern]] property has been added to enable a central specification system to enrich assets with type or manufacturer specification information.

Updated:
* The network cluster-er is extended with the ability to compute different cluster sections in one batch.


---
## Spatial Eye NetCon 2023.1.1.0

First major release. Put into production for Warehouse loads that needed materialized traces to find which busbars are feeding circuit breakers.

---
## Spatial Eye NetCon 2022.4.0.0

First release.

---
