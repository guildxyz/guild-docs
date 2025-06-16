---
hidden: true
---

# How to setup requirements

Requirements are the conditions members must meet to access roles and their rewards.

#### Setting up requirements

**1. Add your first requirement**

* In the role editor, click **"Add requirements"**
* Choose from available requirement types
* Provide the data needed for the requirement
* Edit the requirement image and name, or leave empty to use default settings
* Toggle **"Should not satisfy"** to exclude members who meet this requirement\


**2. Configure requirement logic**

* **"Should meet ALL"** - Members must satisfy every requirement (AND logic)
* **"Should meet 1"** - Members need to satisfy at least one requirement (OR logic)
* **"Should meet X out of Y"** - Members need to satisfy a specific number of requirements



**3. Save and test**

* Click **"Save"**
* Use **"View page as a visitor"** to test the verification process



#### How verification works for members:

* Requirements are checked when members click **"Verify"**
* If they haven't connected a required account, they will see a **"Connect Discord"** button (or Twitter, wallet, etc.)
* Members can clearly see which requirements they have met and which they haven't

{% hint style="info" %}
Most requirements sync constantly - if someone stops meeting a requirement after getting the role, they automatically lose access.
{% endhint %}

#### Common mistake to avoid

**Adding requirements to existing roles:** If you add new requirements to a role that members already have, all current members will lose access to that role since they likely don't meet the new requirement. Create a new role instead or notify members before making changes.



