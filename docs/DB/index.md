## Data Base

![ERD](https://b19kiit.github.io/TGS_IMS/images/update26th.PNG)

### Entities (Node Representation)

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

> - `Item.name` Name of the Item

> - `Item.type` Type of the item being stored

> - `Item.quantity` Total quantity items present in cells of all Store and all inventories.

> - `Item.unknown_quantity` Quantity of extra items, which are not registered to any storage cell, and these items may or may not be present in some inventory.

> - `Item.shelf_life` Time required by the item to get expired.

**Cell** It represents nodes with label `Cell`. A cell is the smallest partition of physical storage space.
A `cell` must belong to exactly one Node `Store`.

A `cells` can be related to `Item` via `Property` node. This will be essential in multiple scenarios, such as evaluating the number of items that can be stored in the cell or check the health of a cell for items stored in them in realtime.

> - `Cell.type` It defined the type of a cell, such as 'gas_cylinder', 'shelf', 'refrigerator' etc

> - `Cell.location` This string describes the physical location of the represented storage unit.

> - `Cell.location_tags` This is an Array of strings that allows segregation & perhaps search with queries of the physical location.


**Property**
