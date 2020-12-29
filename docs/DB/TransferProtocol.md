# TransferProtocol

Transfer Protocol is meant to represent a set of operations as relational data, which are required when Stored Items of an Inventory are being transferred to another Inventory.

To represent the operations we use JSON notation, which can be stored as BSON for more efficient storage in the field `TransferProtocol.protocol`.

## `TransferProtocol.protocol`

As per the current design, we have the following types of operations available:-

1. Filteration: Filter out the items which may not be transferred.

2. Report Generation: Generate reports based on available data.

The *data* required can be availed from the nodes related to the Warehouse.
**The fields in this dataset are generated as per a wide table setup**, doing so simplifies the reprsentation of expressions in filters & report generators.

**Example for item_dataset (IDS)**

IDS selected items table

| .sr_no| .item_number| .quantity| .Item.name| .Item.type     | .Item.quantity (total in warehouse)| .Item.known_quantity| .Item.unknown_quantity| .Item.Cost_per_unit| .cost |
|---|:---|---|---|---|---|---|---|---|---|
| 1     | 1234567789  | 1        | Battery   | ElectricSolid  | 1000       | 999 | 1| 50| 50 |
| 2     | 1234567790  | 1        | Battery   | ElectricSolid  | 1000       | 999 | 1| 50| 50 |
| 3     | 1234567791  | 1        | Battery   | ElectricSolid  | 1000       | 999 | 1| 50| 50 |
 
IDS SUM table ($SUM)
| .quantity | .cost|
|---|:---|
| 230 | 11500|

IDS unique items table ($ITEMS)
|.name|.quantity|.cost|
|---|:---|---|
|Battery|230|11500|
 
### Filter

**Example**
```json
{
  "type": "filter",
  "exclusion_param": {
    "<field_name>": "<value>",
    "<field_name>": { "<": "<value>"},
    "<field_name>": { ">": "<value>"}
  },
  "inclusion_param": {
    "<field_name>": { "!": "<value>"}
  }
}
```

`exclusion_param` are the set of parameter in filter which filter out the items, and the items filtered out will not be transfered.

`inclusion_param` are the set of parameter in filter select the items (filter in) & items filtered in will be transfered to the final inventory.

### Report Generation

**Example**
```js
{
  "type": "reporter",
  "printable": {
    "template_file_id": "ljnas2hf98h.ohnofnoe.infw3=.Sop"   // file_key in TSG FileStore system this must be a .md file
    "replace" : {
      "{company_name}" : {"#const" : "Bharat Steel"},
      "{vendor_name}" : {"#var" : "$UI.vendor_name"},  // fields represent by $UI are manually added by the user
      "{total_cost}" : {
        "#expr" : {"#var" : "$IDS.$SUM.cost"}          // $IDS.$SUM.cost is sum of all items in the IDS table
      }
      "{item_table}" : {
        "#table" :{
          //'Item Name' & 'Worth' will be the header fields of the table
          "Item Name": "$IDS.$ITEMS.name",         //name of specific items
          "Worth": "$IDS.$ITEMS.cost"              //cost of specific items
        }
      }
    }
  }
}
```
