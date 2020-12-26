## Data Base

![ERD](https://b19kiit.github.io/TGS_IMS/images/update26th.PNG)

### Entities (Node Representation)

- **User:** It represents nodes with label `User`, and stores `{ username, _id }` of the users in the system. 

> - `User._id` the unique ID used to represent an User

> - `User.username` the username of the user which may or may not change overtime.

- **Member:** It represents nodes with label `Member`, and stores `{ type, added }` to denote an user's access to a WareHouser.

> - `Member.type` This string defined user's membership in a WareHouse, depending on which the User can access the sytem.

> - `Member.added` This represents UNIX Appx. time in milliseconds, when the user's Membership was created

**WareHouse:** It represents nodes with label `WareHouse`, This entity makes TGS_IMS a fully integrated suit, It is the pivote of relation between the Users, Inventories & Stores/Storages etc. It ensured essentional isolation of data between multiple parties.

It Stores {name, type, location, location_tags}

> - `WareHouse.location` It stores location as String

> - `WareHouse.location_tags` Stores tags as Array of String for segregation of locations

**Inventory:** This entity makes TGS_IMS a fully integrated suit, It is the pivote of relation between the Users, Inventories & Stores/Storages etc. It ensured essentional isolation of data between multiple parties.

It Stores {name, type, tags}

> - `Inventory.type` Type the inventory, primaryly identifies the operational features required on the Inventory

> - `Inventory.tags` Array of String, meant to segregation & searching of Inventories

**Store:**

**Unit:**

**Item:**

**Cell**

**Property**
