# Introduction
     // To be filled
# Overview of index.yml (Current version)
    // To be filled
# Template metadata generator
This tool generates the variable metadata for the given user template using provider metadata. The details of variable metadata can be found in below table.
## Note: 

1. The existing index.yml generator tool has to be integrated into this repo's workflow action. (Ownership: Vincent / Sean Sundberg)
2. Template metadata extractor tool has to integrate with existing index.yml generator tool to get following additional information under variables section. (Ownership: TBD)

Following are the details of variables extracted from the template metadata generator:

|Name| Type|Description|
|-------|-------|-------|
|Name     |     string      |Name of the variable|
|Secure     |     bool      |Is the variable secure or sensitive ?|
|Value      |     string      |Value of variable|
|Type     |     string      |Type of the variable,|
|Description     |     string      |"description of variable1"|
|Source      |     string      |<Resource/Datasource/module Name>.<Resource/Datasource/module Identifier>|
|AttributeName     |     string      |Name of provider argument to which variable is mapped to. If attribute name is terraform core specific like count ignore Provider related Data|
|Required     |     bool      |Is the variable Required argument in provider schema|
|Default     |     bool      |Default value of variable|
|Computed     |     bool      |Is the variable Computed attribute in provider schema|
|Immutable     |     bool      |Is variable forceNew argument in provider schema.|
|Elem     |     provider schema struct      |Child arguments of complex variable types|
|MaxItems     |     int      |Maximum allowed items for list or set type variable. Validation defined in provider schema.|
|MinItems     |     int      |Minimum allowed items for list or set type variable. Validation defined in provider schema|
|Deprecated     |     bool      |Is the variable Deprecated in provider schema.|
|MinValue     |     string      |Minimum value of variable. provider validation for type int values|
|MaxValue     |     string      |Maximum value of variable. provider validation for type int values|
|Options     |     list(string)     |Allowed values of a variable|
|Matches     |     string      |The regex for the variable value.|
|MinValueLength     |     int      |The minimum length of the variable value. provider validation for type string values|
|MaxValueLength|     int      |The maximum length of the variable value. provider validation for type string values|
|CloudDataType     |     string      |Cloud Datatype of a variable. Supported values:`Region`, `ResourceInstance`, `CRN`, `Tags`, `ResourceGroup`|
|CloudDataRange     |     string      |Cloud Data range for a given cloud datatype. For ResourceInstance datatype resource range will be ["service:<service_name Eg:internet-svcs>","resource_group:group_id"]|
|Aliases     |     list      |The list of aliases for the variable name,|
|Hidden     |     bool      |If **true**, the variable is not displayed on UI or Command line.|
|Position     |     int      |The relative position of this variable in a list.|
|GroupBy     |     string      |Group Variables based on services/resource/datasources|

## References:
Detailed index.yml after adding metadata from extractor tool.
https://github.com/kavya498/terraform-ibm-object-storage/blob/gh-pages/index.yaml