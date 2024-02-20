### 5.6.4 Load Factors for WeekBasedCapacityGroup

The feature “load factors” allows suppliers to model and represent otherwise impossible capacity occurrences, by introducing a numerical multiplication factor, that can change the way how a capacity group MUST be interpreted. 

Suppliers MAY apply load factors within a `WeekBasedCapacityGroup`. If they choose to do so, a load factor MUST be applied to every `MaterialDemand` linked by the `WeekBasedCapacityGroup`.

If a ` WeekBasedCapacityGroup ` links several ` MaterialDemand` which contain the same material, load factors applied to those ` MaterialDemand` SHOULD be identical.

Load factors SHOULD be used to solve the following two problems:
-    Usage of non-homogeneous material variants within a capacity group, resulting in diverging capacity utilization.
-    Requirement for having a different unit of measure within a `WeekBasedCapacityGroup`, as opposed to its linked `MaterialDemand`.

Load factors solve these problems by:
- scaling the weekly demand linearly if a material veriant causes higher than normal load within the capacity group. In the simplest cases the load factor expresses a surcharge of, for example, 90% or 150%.
- acting as conversion factors, converting the unit of measure of a `MaterialDemand` into the unit of measure of the ` WeekBasedCapacityGroup`. This conversion result in a “time” (unit:secondUnitOfTime) or a “cycle” (unit:cycle) conversion. Expressing that, for example, a piece of material takes 12 seconds or a set of material takes half a cycle to manufacture.

A load factor of 1 is neutral and leaves the linked `MaterialDemand` unchanged.
Because load factors are applied via the `WeekBasedCapacityGroup` a `MaterialDemand` can have multiple load factors applied to it, that differ from each other.
Without load factors applied the unit of measure of a `WeekBasedCapacityGroup` and its linked `MaterialDemand` SHOULD be identical. With load factors applied the MAY differ.
Lot size restrictions, especially lot size = 1, are not considered when using load factors. Rounding any fractional conversion results SHOULD be avoided to keep demand-capacity comparison consistent.
