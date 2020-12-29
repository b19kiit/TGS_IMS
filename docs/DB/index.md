## Data Base

![ERD](https://b19kiit.github.io/TGS_IMS/images/update26th.PNG)

### Entities (Node Representation)

<hr>

**User:** It represents nodes with label `User`, and stores `{ username, _id }` of the users in the system. 

> - `User._id` the unique ID used to represent an User

> - `User.username` the username of the user which may or may not change overtime.

**Member:** It represents nodes with label `Member`, and stores `{ type, added }` to denote an user's access to a WareHouser.

> - `Member.type` This string defined user's membership in a WareHouse, depending on which the User can access the sytem.

> - `Member.added` This represents UNIX Appx. time in milliseconds, when the user's Membership was created

**WareHouse:** It represents nodes with label `WareHouse`. This entity makes TGS_IMS a fully integrated suit, It is the pivote of relation between the Users, Inventories, Items & Stores. It ensured essentional isolation of data between multiple parties.

It Stores {name, type, location, location_tags}

> - `WareHouse.location` It stores location as String

> - `WareHouse.location_tags` Stores tags as Array of String for segregation of locations

**Inventory:** It represents nodes with label `Inventory`. An Invenotry is a ***collection of Stored-Items***.

It Stores {name, type, tags}

> - `Inventory.type` Type the inventory, primaryly identifies the operational features required on the Inventory

> - `Inventory.tags` Array of String, meant to segregation & searching of Inventories in the WareHouse.

**Store:** It represents nodes with label `Store`. A `Store` belongs to **a** `WareHouse`,
it basically represents a collection of cells (The smallest partition of physical storage space).

It Stores {name, location, location_tags}

> - `Store.location` It stores location as String, a location that provides a more precise location representation of the Store's Warehouse.

> - `Store.location_tags` Array of String, meant to segregation & searching of the location of the Stores in a WareHouse.

**Unit:** It represents nodes with label `Unit`. Stores units for quantitative references or quantitative representation of Properties.
A `Unit` will belong to **a** `WareHouse`,
however, all `WareHouse` will have the same some `Unit`(s) and their conversion functions pre-allotted, for the more swift setup of a WareHouse.

It Stores {name, description}

**Item:** It represents nodes with the label `Item`. Stores details & description of items that can be added to `Inventory`, `Store`, or both.

For Example: If we have an inventory and a store (which represents physical storage) to store a Physical Item 'Li+ Battery', for this item we will add a Node with label `Item` with its {name:'Li+Battery', type:'finished_supply', quantity:0, ...so on}

It Stores {name, type, quantity, known_quantity, unknown_quantity, shelf_life}

> - `Item.name` Name of the Item

> - `Item.type` Type of the item being stored

> - `Item.quantity` Total quantity items present in cells of all Store and all inventories.

> - `Item.unknown_quantity` Quantity of extra items, which are not registered to any storage cell, and these items may or may not be present in some inventory.

> - `Item.shelf_life` Time required by the item to get expired.

**Cell:** It represents nodes with label `Cell`. A cell is the smallest partition of physical storage space.
A `cell` must belong to exactly one Node `Store`.

A `cells` can be related to `Item` via `Property` node. This will be essential in multiple scenarios, such as evaluating the number of items that can be stored in the cell or check the health of a cell for items stored in them in realtime.

It Stores {type, location, location_tags}

> - `Cell.type` It defined the type of a cell, such as 'gas_cylinder', 'shelf', 'refrigerator' etc

> - `Cell.location` This string describes the physical location of the represented storage unit.

> - `Cell.location_tags` This is an Array of strings that allows segregation & perhaps search with queries of the physical location.

**Property:** It represents nodes with label `Property`.
This node stores quantitative-quality & other characteristics, which are quite a pivotal relating 'Item' nodes & `Cell` Nodes, for performing analytical & real-time operations with the data.

And each `Property` node has one & only one `ITEM_PROPERTIES` or `CELL_PROPERTIES` Relation. *A property node can not be shared*

It stores {name, type, value, min, max, normal}

> - `Property.name` Name of the quality, must be unique for a related cell or a related Item.

> - `Property.type` 'quality'| 'range'| 'safety_range'...

> - `Property.value` This can be a string or a Number, depending on the Property. This field is meant for live values of Cell.

> - `Property.min`(optional) This must be a number, which defines the lower boundary for `Property.value`.

> - `Property.max`(optional) This must be a number, which defines upper boundary for `Property.value`.

> - `Property.normal`(optional) This can be a string or a Number, for representing desirable `Property.value`.

**ItemStored:** It represents nodes with label `ItemStored`.
This node stores entry for an item added an Inventory and/or physically added to a cell of a store.

It stores {quantity, expires, added_on, engaged, custom_tags}

> - `ItemStored.quantity` Numeric value to represent quantity, if it means anything to Item stored. *Default value is 1*

> - `ItemStored.expires` UNIX_AXP time at which the stored item will expire

> - `ItemStored.added_on` UNIX_AXP time, when the stored_item expires

> - `ItemStored.engaged` IF the item is engaged, it can not be used for any other purpose.

> - `ItemStored.custom_tags` Array of strings if required.

**BillOfMaterial:** It represents nodes with lable `BillOfMaterial`.
It stores the recipe for creating a Bill of items, using the Items present in the Warehouse.

It stores {name, created_on, updated_on}

> - `BillOfMaterial.name` Name as String for the BillOfMaterial

> - `BillOfMaterial.created_on` UNIX_AXP time ms

> - `BillOfMaterial.created_on` UNIX_AXP time ms

**TransferProtocol:** It represents nodes with lable `TransferProtocol`.
Every systematic transfer of Items from one Inventory to another, will follow a customized Protocol for Transfer.

This node will prescribe operations such as 'filteration', 'identification of specific items', 'report generation' & 'chalan generation' etc.

> - `TransferProtocol.name` Name as String for the TransferProtocol, default = name_of_inital_inventory + '_to_' + name_of_final_inventory

> - `TransferProtocol.min_limit` Minimum number of Item required to follow this protocol

> - `TransferProtocol.max_limit` Maximim number of Item allowed in this protocol

> - `TransferProtocol.protocol` JSON representation of the protocol algorithm.

[More About TransferProtocol](./TransferProtocol)

**Cost:**

**HsnRegister:**

<br>

<hr>

### Relations

<hr>

**MEMBERSHIPS:** Connects A `User` node with multiple `Member` nodes.
Representing a user's access to a `Warehouse` via a `Member` node.

<br>

**MEMBERS:** Connects A `Warehouse` node with one or more `Member` nodes. (All Warehouse must have at least one Member as {'type':'admin'})
Representing `Member` nodes related to a `Warehouse`.

> Members of a Warehouse, with at least one admin.

<br>

**INVENTORIES:** Connects A `Warehouse` node with multiple `Inventory` nodes.
Representing `Inventory` nodes related to a `Warehouse`.

> Inventories in a Warehouse.

<br>

**STORES:** Connects A `Warehouse` node with multiple `Store` nodes.

> Stores in a Warehouse.

<br>

**UNITS:** Connects A `Warehouse` node with multiple `Unit` nodes.

> Units in a Warehouse.

<br>

**ITEMS:** Connects A `Warehouse` node with multiple `Item` nodes.

> Items registered in a Warehouse

<br>

**CELLS:** Connects A `Store` node with multiple `Item` nodes.

> Cells present in a store.

<br>

**STORED_ITEMS:** Connects A `Inventory` node with multiple `ItemStored` nodes.

> Items present in an Inventory

<br>

**ITEM_STOREDS:** Connects A `Item` node with multiple `ItemStored` nodes.

> Items which have been stored physcially or have been added to some inventory.

<br>

**STORED_IN:** Connects a `StoredItem` to a `Cell` node.

> Represents where a stored Item is keeps physically

<br>

**UNIT_OF_MEASURE:** A relation with an `Unit` node, for representing some measurement.

**UNITS_OF(CONCEPTUAL):** This represents a measurement using the `Unit` nodes present in the `Warehouse`. It stores {value:Number<Float>}

<br>

**ITEM_PROPERTIES:** Connects a `Item` node with a `Property` nodes. And each `Property` node has one & only one `ITEM_PROPERTIES` or `CELL_PROPERTIES` Relation.

<br>

**CELL_PROPERTIES:** Connects a `Cell` node with a `Property` nodes. And each `Property` node has one & only one `ITEM_PROPERTIES` or `CELL_PROPERTIES` Relation.

<br>

**CONVERSION_FUNCTIONS:** It Connects a `Unit` node to another `Unit` node. It stores {formula:String<JS VM executable code>}

These relations store the procedures for conversion of value for one Unit to another one.

<br>

**TRANSFER_PROTOCOL:** It Connects a `Inventory` node miltiple `TransferProtocol` nodes.

<br>

**TRANSFER_TO:** It Connects a `TransferProtocol` node an `Inventory` node.
It reprsents the final Inventory for the items being transfered.

<br>

