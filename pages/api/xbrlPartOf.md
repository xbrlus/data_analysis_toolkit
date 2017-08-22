---
title: xbrlPartOf REST API
keywords: api
summary: "This API allows the user to get all the parent elements that an element is part of across all networks in the filing."
sidebar: api_sidebar
permalink: xbrlPartOf.html
folder: api
---
The API requires the element name and the filing number. The API will return all calculation parents of the specified element plus attributes such as weight, the effective weight, the leaf node, balance type and associated network.

This function is used when a user want to determine what elements a specified element is part of.

### **Sample URL**
 In the sample URL below, replace text "EnterKeyHere" (without quotes) with your API key to return data in your browser window:

  <http://csuite.xbrl.us/php/dispatch.php?Task=xbrlPartOf&AccessionID=135173&Element=ProfitLoss&API_Key=EnterKeyHere>

### **Method**

  The API supports the following

  `GET` | `POST`

### **URL Params**

   **Required:**

  `TASK=xbrlPartOf`

  `API_Key=[uuid]` - A valid API Key must be provided. This is freely available from XBRL US at <http://xbrl.us/apirequest>

  `AccessionID=[int] OR Accession=[alpha]` - AccessionID: Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

  - Accession: SEC Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter allows a comma separated list.

  `Element=[alphanumeric]` - The element name in the base taxonomy. This parameter will **not** take a comma separated list.


   **Optional:**

  `AccessionID=[int]` - Internal Accession identifier used by the XBRL US database. This is a unique filing identifier. For example one company will have many filings. This is returned by the API and can be used in subsequent calls. This allows a comma separated list.

  `Accession=[alpha]` - Filing accession number. This is the accession number used as the filing identifier used by the SEC. This parameter allows a comma separated list.

  `DtsName=[alpha]` - The name of the Discoverable Taxonomy Set. If no DTS Name is provided the value defaults to "US GAAP". Allowable values include "US GAAP", "Credit Ratings", "XBRL", "Risk Return", "IFRS", "DEI", "Country", "Currency", "Exchange", "Invest", "NAICS", "SIC", "STPR".

   `DtsID=[int]` - Internal DTS identifier used by the XBRL US database. This is a unique identifier that allows the selection of a standard taxonomy published by a standard setter such as the FASB, or a DTS published by a company.

   `Version=[YYYY]` - Release year of a standard taxonomy. To retrieve the 2017 US GAAP taxonomy the parameters DtsName = "US GAAP"  and Version = "2017" are used.

   `Format=[xml|json]` - Returns the results in a xml or json format. If no parameter is provided then json is returned.


   **Minimum:**

   All calls to the API must include the `Element` parameter name and at least an `AccessionID`, a `DtsName`, a `DtsID` or an `Accession` number. In addition the extended link role should not be used. To get the calculation children of an element in a network use the API xbrlChildren or  xbrlParts end points.


### **Data Params**

  The API supports the same params as the URL.

### **Success Response xml (Normal)**

```xml
    <dataRequest date="2015-10-06T19:34:20-0400">
      <fact>
        <entity>
        <![CDATA[ EXXON MOBIL CORP ]]>
        </entity>
        <accessionID>157992</accessionID>
        <filingAccession>0000034088-16-000065</filingAccession>
        <filingDate>2016-02-24</filingDate>
        <elementName>Assets</elementName>
        <namespace>http://fasb.org/us-gaap/2015-01-31</namespace>
        <abstract>f</abstract>
        <balance>Debit</balance>
        <periodType>Instant</periodType>
        <monetary>true</monetary>
        <childElementName>AssetsCurrent</childElementName>
        <childNamespace>http://fasb.org/us-gaap/2015-01-31</childNamespace>
        <treeDepth>1</treeDepth>
        <treeSequence>1</treeSequence>
        <calculationWeight>1</calculationWeight>
        <calculationEffectiveWeight>1</calculationEffectiveWeight>
        <leafNode>1</leafNode>
        <rootNode>1</rootNode>
        <networkName>000200 - Statement - Consolidated Balance Sheet</networkName>
        <groupURI>
        http://www.exxonmobil.com/role/StatementConsolidatedBalanceSheet
        </groupURI>
    </dataRequest>
```
  `dataRequest - date` - The data request date attribute is the date that the data was generated. It is not the date of the query.  Data is cached once it is requested and is returned from cache if available. The data remains in cache for a day from the request. This means that data could be up to a day old if it has been previously requested.

  `calculationEffectiveWeight` - This is the weight relationship between the element in the request and the element returned in this record. This differs from the calculationWeight which is the weight to the parent element in the calculation tree. Whereas as the calculationEffectiveWeight is the weight relative to the requested element. They will often be the same but will vary as the tree depth increases.

  `leafNode` - This indicates if the element is a leaf on the tree, or a branch. If the value is 0 the element is the last node on the tree (It has no children). If the value is 1 then the element is a branch element that will have children elements.

  `rootNode` - This indicates if the element is a root of the tree, or a branch. If the value is 0 the element is the first node on the tree (The element requested). If the value is 1 then the element is a branch element that will have a parent elements.

### **Success Response json US GAAP 2017 (Normal)**

```json
{
  "fact": [
  {
    "entity": {},
    "accessionID": {},
    "filingAccession": {},
    "filingDate": {},
    "elementName": "NetIncomeLossAvailableToCommonStockholdersBasic",
    "namespace": "http://fasb.org/us-gaap/2017-01-31",
    "abstract": "f",
    "balance": "Credit",
    "periodType": "Duration",
    "monetary": "true",
    "childElementName": {},
    "childNamespace": {},
    "treeDepth": "2",
    "treeSequence": "25",
    "calculationWeight": "0",
    "calculationEffectiveWeight": "1",
    "leafNode": "0",
    "rootNode": "1",
    "networkName": "124000 - Statement - Statement of Income (Including Gross Margin)",
    "groupURI": "http://fasb.org/us-gaap/role/statement/StatementOfIncome"
  },
  {
    "entity": {},
    "accessionID": {},
    "filingAccession": {},
    "filingDate": {},
    "elementName": "NetIncomeLossAvailableToCommonStockholdersDiluted",
    "namespace": "http://fasb.org/us-gaap/2017-01-31",
    "abstract": "f",
    "balance": "Credit",
    "periodType": "Duration",
    "monetary": "true",
    "childElementName": "NetIncomeLossAvailableToCommonStockholdersBasic",
    "childNamespace": "http://fasb.org/us-gaap/2017-01-31",
    "treeDepth": "1",
    "treeSequence": "25",
    "calculationWeight": "1",
    "calculationEffectiveWeight": "1",
    "leafNode": "1",
    "rootNode": "0",
    "networkName": "124000 - Statement - Statement of Income (Including Gross Margin)",
    "groupURI": "http://fasb.org/us-gaap/role/statement/StatementOfIncome"
  }
],
"count": "1"
}
```

### **Error Response**

  An error is returned if no value is defined for an element name.

```xml
    <error>
        <date>Fri, 04 Sep 2015 17:06:50</date>
        <status>Error - Bad Parameter</status>
        <message>
          <![CDATA[
          The value entered for the Element of is not valid.
          ]]>
        </message>
    </error>
```

  An error is returned if an incorrect parameter is provided.

```xml
    <error>
      <date>Fri, 04 Sep 2015 17:08:00</date>
      <status>Error - Bad Parameter</status>
      <message>
        <![CDATA[
        The parameter of mith with a value of 2 is not valid.
        ]]>
      </message>
    </error>
```

  An error is provided if a filing number or CIK is not provided.

```xml
    <error>
      <date>Tue, 06 Oct 2015 19:43:06</date>
      <status>Error - Insufficient Parameters</status>
      <message>
        <![CDATA[
          'This call returns too much data. Please revise the attributes to include at least a network id or accession. Number.
        ]]>
      </message>
    </error>
```



### **Notes**

  Any parameters defined that are not in the list above will result in an error.

### **XBRL Database**

  The API calls the XBRL database using a recursive query. An example of the query is shown below. If you take a copy of the XBRL database or use the public database you can build the same API in your system using this query. Replace the $ variables with the appropriate parameters.

  Example query

```sql
WITH RECURSIVE rels(
  relationship_id
  , network_id
  , from_element_id
  , to_element_id
  , tree_sequence
  , tree_depth
  , dts_id
  , extended_link_qname_id
  , extended_link_role_uri_id
  , description
  , weight
  , calculation_weight)
AS (
WITH ar AS
  (SELECT
    dts_relationship_id as relationship_id
    , n.dts_network_id as network_id
    , from_element_id
    , to_element_id
    , tree_sequence
    , tree_depth
    , n.dts_id
    , n.extended_link_qname_id
    , n.extended_link_role_uri_id
    , n.description
    , calculation_weight
    , calculation_weight
  FROM dts_relationship rel
  JOIN dts_network n ON n.dts_network_id = rel.dts_network_id
  WHERE
   n.extended_link_qname_id = (select qname_id from qname where local_name = 'calculationLink')
   AND n.dts_id $dtsUsed
  )
SELECT
  ar.*
FROM ar
JOIN dts_element ae
  ON ar.dts_id = ae.dts_id and ar.to_element_id = ae.element_id
JOIN element e_to
  ON e_to.element_id = ae.element_id
JOIN qname q_to
  ON q_to.qname_id = e_to.qname_id
WHERE  
  ae.dts_id $dtsUsed
  AND q_to.local_name = '$ElementName'
UNION
SELECT
  r.dts_relationship_id
  , r.dts_network_id
  , r.from_element_id
  , r.to_element_id
  , r.tree_sequence
  , r.tree_depth
  , n.dts_id
  , n.extended_link_qname_id
  , n.extended_link_role_uri_id
  , n.description
  , r.calculation_weight * rels.weight AS weight
  , r.calculation_weight
FROM  rels
JOIN dts_relationship r
  ON r.to_element_id = rels.from_element_id
JOIN dts_network n
  ON r.dts_network_id = n.dts_network_id and rels.dts_id = n.dts_id and n.extended_link_qname_id = rels.extended_link_qname_id
JOIN dts_element ae
  ON n.dts_id = ae.dts_id and r.to_element_id = ae.element_id
)
SELECT
  local_name_from
  ,namespace_from
  ,local_name
  ,namespace
  ,entity_name
  ,filing_date
  , accession_id
  ,filing_accession_number
  ,calculation_weight
  ,calculation_effective_weight
  ,child_balance
  ,child_period_type
  ,child_is_abstract
  ,child_is_monetary
  ,parent_balance
  ,parent_period_type
  ,parent_is_abstract
  ,parent_is_monetary
  ,MAX (CASE WHEN local_name_from = ANY (child) THEN 1 ELSE 0 END) AS root_node_flag
  ,MAX (CASE WHEN local_name = ANY (parent) THEN 1 ELSE 0 END) AS leaf_node_flag
  ,string_agg(tree_depth::text,', ')  AS tree_depth
  , string_agg(tree_sequence::text,', ') AS tree_sequence
  ,string_agg(uri,', ') AS group_uri
  , string_agg(description,'|') AS description

FROM
(SELECT
  qfrm.local_name as local_name_from
  ,qfrm.namespace as namespace_from
  ,qto.local_name
  ,qto.namespace
  ,ac.entity_name
  ,ac.properties->>'filing_date' as filing_date
  ,ac.report_id as accession_id
  ,ac.properties->>'filing_accession_number' as filing_accession_number
  ,rl.calculation_weight
  ,rl.weight as calculation_effective_weight
  ,  CASE
        WHEN elto.balance_id = 1 THEN 'Debit'::text
        WHEN elto.balance_id = 2 THEN 'Credit'::text
        ELSE NULL::text
      END AS child_balance
  , CASE
        WHEN elto.period_type_id = 1 THEN 'Instant'::text
        WHEN elto.period_type_id = 2 THEN 'Duration'::text
        WHEN elto.period_type_id = 3 THEN 'Forever'::text
        ELSE NULL::text
      END AS child_period_type
  , elto.abstract as child_is_abstract
  , CASE
        WHEN elto.is_monetary = 't' THEN 'true'::text
        WHEN elto.is_monetary = 'f' THEN 'false'::text
        ELSE NULL::text
      END as child_is_monetary
  , CASE
        WHEN elfrom.balance_id = 1 THEN 'Debit'::text
        WHEN elfrom.balance_id = 2 THEN 'Credit'::text
        ELSE NULL::text
      END AS parent_balance
  , CASE
        WHEN elfrom.period_type_id = 1 THEN 'Instant'::text
        WHEN elfrom.period_type_id = 2 THEN 'Duration'::text
        WHEN elfrom.period_type_id = 3 THEN 'Forever'::text
        ELSE NULL::text
      END AS parent_period_type
  , elfrom.abstract as parent_is_abstract
  , CASE
        WHEN elfrom.is_monetary = 't' THEN 'true'::text
        WHEN elfrom.is_monetary = 'f' THEN 'false'::text
        ELSE NULL::text
      END as parent_is_monetary
  , tree_depth
  , tree_sequence
  , elruri.uri
  , rl.description
  , array_agg(qto.local_name) OVER (Partition BY ac.report_id) as child
  , array_agg(qfrm.local_name) OVER (Partition BY ac.report_id) as parent
  FROM rels rl
  JOIN element elfrom
    ON elfrom.element_id = rl.from_element_id
  JOIN qname qfrm
    ON qfrm.qname_id = elfrom.qname_id
  JOIN element elto
    ON elto.element_id = rl.to_element_id
  JOIN qname qto
    ON qto.qname_id = elto.qname_id
  LEFT JOIN report ac
    ON ac.dts_id = rl.dts_id
  JOIN uri elruri
    ON rl.extended_link_role_uri_id = elruri.uri_id
  ORDER BY description, tree_sequence
  )  AS all_links
GROUP by 1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18
ORDER BY accession_id, leaf_node_flag, min(description),  min(tree_depth) desc,  min(tree_sequence)
```
