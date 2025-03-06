---
tags:
  - CUT-IN VEHICLE
---

# Aborted vehicle cut-in

**Scenario location:** 
`/$FTX_PACKAGES/base_scenarios/scenarios/vehicle_cut_in/aborted_vehicle_cut_in/`

In the **aborted_vehicle_cut_in** scenario, the cut-in vehicle is driving in a lane adjacent to the Ego. The cut-in vehicle starts performing a cut-in maneuver into the Ego's lane in front of the Ego and suddenly aborts the maneuver and cuts out in the opposite direction from the cut-in maneuver.
For a valid scenario, the cut-in vehicle's invasion of the Ego's lane must be performed in front of the Ego.

## Prerequisites
**Environment requirements:** The road must have two or more lanes.

## Actors

The actors associated with this scenario are as follows:

Name| Description | Type | Depiction |
|-- | -- | -- | -- |
|`ego` | Vehicle under test | `vehicle` |<img src="../../../../actor_images/ego.png" style="width:100px">|
|`cut_in_vehicle` | Cut-in vehicle | `vehicle` |<img src="../../../../actor_images/sedan/white_sedan.png" style="width:100px">  |

## Scenario phases
The phase descriptions are as follows:

### `phase_ego_warm_up`

**Ego:** The Ego starts driving at `ego_speed_at_start` in one lane.

**cut_in_vehicle:** The cut-in vehicle starts driving at `cut_in_vehicle_speed_at_start` in the lane adjacent to the Ego. The cut-in vehicle has an initial lateral lane offset of `cut_in_vehicle_lat_offset_at_start`. At the end of this phase, the cut-in vehicle is ahead of the Ego by `cut_in_vehicle_time_gap_to_ego_at_initial_phase_end`.


### `phase_essence_lane_change` 

**Ego:** The Ego continues driving and attempts to stay in the same lane and maintain the same speed.

**cut_in_vehicle:** The cut-in vehicle performs a cut-in maneuver into the Ego's lane from the left or right lane adjacent to the Ego. At the end of this phase, the cut-in vehicle is ahead of the Ego by `ego_time_gap_to_cut_in_vehicle_at_change_lane_end` and has a lateral lane offset of `cut_in_vehicle_lat_offset_at_lane_change_end`.

### `phase_essence_abort` 

**Ego:** The Ego continues driving and attempts to maintain the same speed.

**cut_in_vehicle:** The cut_in_vehicle aborts the cut-out maneuver and cuts out of the Ego's lane back into the adjacent lane on the side from which it started the cut-in maneuver. At the end of this phase the cut_in_vehicle is back in its target lane and reaches the final lateral offset of `cut_in_vehicle_lat_offset_at_end`. 

### `phase_post` 

**Ego:** The Ego continues driving and attempts to maintain the same speed.

**cut_in_vehicle:** The cut-in vehicle continues driving, attempting to maintain its lane and speed.

## Parameters

!!! Note    
    The common parameters, events, and metrics are available in the [**base_config_file**](../../config/base_generic_base_scenario.md).

The paths to the CSV file and the main CSV file are as follows:

```
/$FTX_PACKAGES/base_scenarios/test_suites/test_suite_definitions/vehicle_cut_in/aborted_vehicle_cut_in.csv
/$FTX_PACKAGES/base_scenarios/test_suites/test_suite_definitions/vehicle_cut_in/aborted_vehicle_cut_in_main.csv
```

The parameters you can constrain to create tests with the **aborted_vehicle_cut_in.csv** file are as follows:

[//]: # ($$input)

Parameter | Description | Range
-- | -- | --
`gen_cut_in_vehicle_lat_offset_at_lane_change_end` | Lateral offset of the cut_in_vehicle at the end of phase_essence_lane_change | [-1..1]m
`gen_cut_in_vehicle_speed_at_start` | Input speed of the cut_in_vehicle at the start | [0..150]kph
`gen_cut_in_vehicle_rel_speed_to_ego_at_start` | Input relative speed of the cut_in_vehicle at the start | [-10..10]kph
`gen_cut_in_side` | Input side from which the vehicle cuts in | left, right
`gen_ego_time_gap_to_cut_in_vehicle_at_change_lane_start` | Input time gap between the Ego and the cut_in_vehicle at the start of lane change | [1..5]s
`gen_ego_time_gap_to_cut_in_vehicle_at_change_lane_end` | Input time gap between the Ego and the cut_in_vehicle at the end of lane change | [1..5]s
`gen_cut_in_vehicle_lat_offset_at_start` | Lateral offset of the cut_in_vehicle at start | [-1..1]m
`gen_cut_in_vehicle_lat_offset_at_end` | Lateral offset of the cut_in_vehicle at end | [-1..1]m
`gen_ego_speed_at_start` | Input speed of the Ego | [0..150]kph

[//]: # ($$input)

[//]: # ($$metrics)

## Metrics
Metrics collected during test execution are given below.

### Coverage
The coverage metrics are given below.

#### Coverage items
The multi-dimensional situations captured during the test execution are as follows:


[//]: # ($$coverage)

Item | Description | Range | Unit/Type
-- | -- | -- | --
`ego_lon_distance_to_cut_in_vehicle_at_abort_end` | How far ahead is the cut_in_vehicle relative to Ego at the end of phase_essence_abort | [0..0.5), [0.5..1), [1..1.5), [1.5..2), [2..2.5), [2.5..3), [3..3.5), [3.5..4), [4..4.5), [4.5..5), [5..6), [6..7), [7..8), [8..9), [9..10), [10..11), [11..12), [12..13), [13..14), [14..15), [15..20), [20..25), [25..30), [30..35), [35..40), [40..45), [45..50), [50..55), [55..60) | m
`ego_speed_at_abort_end` | Speed of the Ego at the end of phase_essence_abort | [0..150), every: 10.0 | kph
`initial_phase_duration` | Duration of the entire phase_ego_warm_up | [2..8), every: 1.0 | s
`lane_change_duration` | Duration of the entire phase_essence_lane_change | [3..7), every: 1.0 | s
`abort_duration` | Duration of the entire phase_essence_abort | [3..6), every: 1.0 | s
`ego_rel_speed_to_cut_in_vehicle_at_abort_end` | Relative speed of the cut_in_vehicle to the Ego at the end of phase_essence_abort | [-70..30), every: 10.0 | kph
`cut_in_vehicle_max_lat_offset_to_lane_center_at_lane_change` | How deep the cut_in_vehicle goes into Ego-lane before it decides to get back to its lane | [-1..1), every: 0.5 | m
`cut_in_vehicle_mean_acceleration_at_lane_change_phase` | The mean acceleration of the cut_in_vehicle during phase_essence_lane_change | [-2..2), every: 0.2 | mpsps
`cut_in_vehicle_lat_offset_at_lane_change_end` | Lateral offset of the cut_in_vehicle at the end of phase_essence_lane_change | [-1..1), every: 0.5 | m
`cut_in_vehicle_mean_acceleration_at_abort_phase` | The mean acceleration of the cut_in_vehicle during phase_essence_abort | [-2..2), every: 0.2 | mpsps
`gen_cut_in_vehicle_lat_offset_at_lane_change_end` | Lateral offset of the cut_in_vehicle at the end of phase_essence_lane_change | [-1..1), every: 0.5 | m

<details markdown="1">

<summary>[Click] The coverage items inherited from the <b>sut.vehicle_cut_in_common</b> scenario are as follows:</summary>

Item | Description | Range | Unit/Type
-- | -- | -- | --
`cut_in_variant` | The variant of the cut_in scenario family | vehicle_cut_in, aborted_cut_in, non_smooth_cut_in, cut_in_out_of_traffic, double_cut_in | cut_in_variant
`cut_in_vehicle_speed_at_scenario_start` | Speed of the cut_in_vehicle at start | [0..150), every: 10.0 | kph
`cut_in_vehicle_position_to_ego` | The position and speed of the cut_in_vehicle wrt Ego at the start | cut_in_vehicle_is_behind_and_faster, cut_in_vehicle_is_ahead_and_slower | cut_in_vehicle_position_to_ego
`cut_in_vehicle_speed_at_scenario_end` | Speed of the cut_in_vehicle at the end | [0..150), every: 10.0 | kph
`gen_cut_in_vehicle_speed_at_start` | Input speed of the cut_in_vehicle at the start | [0..150), every: 10.0 | kph
`cut_in_vehicle_speed_at_start` | Speed of the cut_in_vehicle at the start | [0..150), every: 10.0 | kph
`gen_cut_in_vehicle_rel_speed_to_ego_at_start` | Input relative speed of the cut_in_vehicle at the start | [-10..10), every: 10.0 | kph
`cut_in_vehicle_rel_speed_to_ego_at_start` | Relative speed of the cut_in_vehicle at the start | [0..150), every: 10.0 | kph
`gen_cut_in_side` | Input side from which the vehicle cuts in | left, right | av_side
`gen_ego_time_gap_to_cut_in_vehicle_at_change_lane_start` | Input time gap between the Ego and the cut_in_vehicle at the start of lane change | [1..5), every: 0.5 | s
`gen_ego_time_gap_to_cut_in_vehicle_at_change_lane_end` | Input time gap between the Ego and the cut_in_vehicle at the end of lane change | [1..5), every: 0.5 | s
`gen_cut_in_vehicle_lat_offset_at_start` | Lateral offset of the cut_in_vehicle at start | [-1..1), every: 0.5 | m
`cut_in_vehicle_lat_offset_at_start` | Lateral offset of the cut_in_vehicle at start | [-1..1), every: 0.5 | m
`gen_cut_in_vehicle_lat_offset_at_end` | Lateral offset of the cut_in_vehicle at end | [-1..1), every: 0.5 | m
`ego_distance_to_cut_in_vehicle_at_change_lane_start` | How ahead is the cut_in_vehicle relative to the Ego at change_lane start | [0..0.5), [0.5..1), [1..1.5), [1.5..2), [2..2.5), [2.5..3), [3..3.5), [3.5..4), [4..4.5), [4.5..5), [5..6), [6..7), [7..8), [8..9), [9..10), [10..11), [11..12), [12..13), [13..14), [14..15), [15..20), [20..25), [25..30), [30..35), [35..40), [40..45), [45..50), [50..55), [55..60) | m
`ego_speed_at_change_lane_start` | Speed of the Ego at change_lane start | [0..150), every: 10.0 | kph
`cut_in_vehicle_rel_speed_to_ego_at_change_lane_start` | How much faster is the cut_in_vehicle relative to the Ego at change_lane start | [-70..30), every: 10.0 | kph
`ego_lane` | Relative Ego lane within road (innermost/middle/outermost) | innermost, outermost, middle | lane_relative_side
`cut_in_vehicle_cuts_in_from_side` | The cut_in_vehicle cuts-in from left/right of the Ego | left, right | av_side
`ego_relative_time_distance_to_cut_in_vehicle_at_change_lane_start` | Ego relative time distance to the cut_in_vehicle at change lane start | [-6..6), every: 0.5 | s
`road_curvature_at_change_lane_start` | Curvature of the road at change lane start | other, straightish, soft_left, hard_left, soft_right, hard_right | curvature
`cut_in_vehicle_lat_offset_at_cut_in_start` | Lane offset of the cut_in_vehicle at start of cut_in phase | [-1..1), every: 0.5 | m
`cut_in_side` | The side from which the vehicle cuts in | left, right | av_side
`ego_time_gap_to_cut_in_vehicle_at_change_lane_start` | Ego time gap to the cut_in_vehicle at the start of lane change | [1..5), every: 0.5 | s
`ego_distance_to_cut_in_vehicle_at_change_lane_end` | How far ahead is the cut_in_vehicle relative to the Ego at change_lane end | [0..0.5), [0.5..1), [1..1.5), [1.5..2), [2..2.5), [2.5..3), [3..3.5), [3.5..4), [4..4.5), [4.5..5), [5..6), [6..7), [7..8), [8..9), [9..10), [10..11), [11..12), [12..13), [13..14), [14..15), [15..20), [20..25), [25..30), [30..35), [35..40), [40..45), [45..50), [50..55), [55..60) | m
`ego_speed_at_change_lane_end` | Speed of the Ego at change_lane end | [0..150), every: 10.0 | kph
`cut_in_vehicle_rel_speed_to_ego_at_change_lane_end` | How much faster is the cut_in_vehicle relative to the Ego at change_lane end | [-70..30), every: 10.0 | kph
`ego_relative_time_distance_to_cut_in_vehicle_at_change_lane_end` | Ego relative time distance to the cut_in_vehicle at change lane end | [-6..6), every: 0.5 | s
`cut_in_duration` | The time taken by the cut_in_vehicle to perform the cut_in | [0.5..3), every: 0.5 | s
`cut_in_vehicle_lat_offset_at_cut_in_end` | Lane offset to the cut_in_vehicle at end of cut_in phase | [-1..1), every: 0.5 | m
`ego_time_gap_to_cut_in_vehicle_at_change_lane_end` | Ego time gap to the cut_in_vehicle at the end of lane change | [1..5), every: 0.5 | s
`ego_slowed_down` | Did the Ego slow down | true, false | bool
`cut_in_vehicle_lat_offset_at_end` | Lateral offset of the cut_in_vehicle at end | [-1..1), every: 0.5 | m

</details>

<details markdown="1">

<summary>[Click] The coverage items inherited from the <b>sut.generic_base_scenario</b> scenario are as follows:</summary>

Item | Description | Range | Unit/Type
-- | -- | -- | --
`curve_road_direction` | Direction of the road curvature | left_curve, right_curve, neither | curve_direction
`min_road_element_radius` | Minimum radius of the road | [0..100), [100..150), [150..200), [200..300), [300..400), [400..600), [600..800), [800..1000), [1000..1200), [1200..1400), [1400..1600), [1600..1800), [1800..2000), [2000..2400), [2400..2800), [2800..3200), [3200..3600), [3600..4000), [4000..5000), [5000..6000), [6000..8000), [8000..10000), [10000..20000) | m
`max_road_element_radius` | Maximum radius of the road | [0..100), [100..150), [150..200), [200..300), [300..400), [400..600), [600..800), [800..1000), [1000..1200), [1200..1400), [1400..1600), [1600..1800), [1800..2000), [2000..2400), [2400..2800), [2800..3200), [3200..3600), [3600..4000), [4000..5000), [5000..6000), [6000..8000), [8000..10000), [10000..20000) | m
`ego_speed_on_curve_road_element` | Speed of the Ego on the curved road | [0..150), every: 10.0 | kph
`main_road_type` | The type of road in the scenario on which the Ego was driving | none, off_highway, highway, junction, merging_lane | road_type_list
`avg_curve_radius` | Average curve radius throughout the scenario | [0..4900), every: 150.0 | m
`road_element_sign_type` | Type of traffic signal | stop, yield, other | traffic_sign_kind
`ego_road_element_max_lanes` | Maximum number of lanes on which the Ego is travelling | [1..6), every: 1.0 | uint
`ego_road_element_min_lanes` | Minimum number of lanes on which the Ego is travelling | [1..6), every: 1.0 | uint
`ego_road_element_legal_speed` | Ego's legal speed on the road element | [5.0..9.0), [9.0..10.0), [10.0..12.0), [12.0..15.0), [15.0..20.0), [20.0..25.0), [25.0..30.0), [30.0..35.0), [35.0..40.0), [40.0..45.0), [45.0..46.0), [46.0..50.0), [50.0..55.0), [55.0..57.0), [57.0..58.0), [58.0..60.0), [60.0..62.0), [62.0..65.0), [65.0..70.0), [70.0..75.0) | kph
`vanishing_lane` | Did vehicle enter the vanishing lane | true, false | bool
`emerging_lane` | Did vehicle enter the emerging lane | true, false | bool
`gen_ego_speed_at_start` | Input speed of the Ego | [0..150), every: 10.0 | kph
`ego_speed_at_start` | Actual speed of the Ego at the start of the scenario | [0..150), every: 10.0 | kph

</details>

[//]: # ($$coverage)


#### Cross coverage items
The test execution data for the combination of multiple coverage items is as follows:

[//]: # ($$cross_coverage)

Item | Description | Referred coverage items
-- | -- | -- 
`cross_lane_change_duration_and_ego_lon_distance_to_cut_in_vehicle_at_abort_end` | Cross of the duration of the lane change phase with the relative distance between the Ego and the cut-in vehicle at the end of the abort phase | lane_change_duration, ego_lon_distance_to_cut_in_vehicle_at_abort_end

<details markdown="1">

<summary>[Click] The cross coverage items inherited from the <b>sut.vehicle_cut_in_common</b> scenario are as follows:</summary>

Item | Description | Referred coverage items
-- | -- | -- 
`cross_ego_lane_cut_in_vehicle_cuts_in_from_side` | Cross coverage of ego_lane and cut_in_side | ego_lane, cut_in_vehicle_cuts_in_from_side
`cross_ego_distance_to_cut_in_vehicle_at_change_lane_start_ego_speed_at_change_lane_start` | Cross of the Ego distance to cut_in_vehicle and Ego speed at start of phase_essence_change_lane | ego_distance_to_cut_in_vehicle_at_change_lane_start, ego_speed_at_change_lane_start
`cross_ego_distance_to_cut_in_vehicle_at_change_lane_start_cut_in_side` | Cross of the Ego distance to cut_in_vehicle at change lane start and cut in side | ego_distance_to_cut_in_vehicle_at_change_lane_start, cut_in_vehicle_cuts_in_from_side
`cross_cut_in_vehicle_rel_speed_to_ego_at_change_lane_start_cut_in_side` | Cross of the relative speed at change lane start and cut in side | cut_in_vehicle_rel_speed_to_ego_at_change_lane_start, cut_in_vehicle_cuts_in_from_side
`cross_ego_speed_at_change_lane_start_cut_in_side` | Cross of the Ego speed at change lane start and cut in side | ego_speed_at_change_lane_start, cut_in_vehicle_cuts_in_from_side
`cross_ego_distance_to_cut_in_vehicle_at_change_lane_start_cut_in_vehicle_rel_speed_to_ego_at_change_lane_start_cut_in_side` | Cross of the Ego distance to cut_in_vehicle at change lane start and relative speed at start of phase_essence_change_lane and cut in side | ego_distance_to_cut_in_vehicle_at_change_lane_start, cut_in_vehicle_rel_speed_to_ego_at_change_lane_start, cut_in_vehicle_cuts_in_from_side
`cross_ego_distance_to_cut_in_vehicle_at_change_lane_start_cut_in_vehicle_rel_speed_to_ego_at_change_lane_start_ego_speed_at_change_lane_start_cut_in_side` | Cross of the Ego distance to cut_in_vehicle at change lane start and relative speed at change lane start and Ego speed at change lane start and cut in side | ego_distance_to_cut_in_vehicle_at_change_lane_start, cut_in_vehicle_rel_speed_to_ego_at_change_lane_start, ego_speed_at_change_lane_start, cut_in_vehicle_cuts_in_from_side
`cross_cut_in_duration_ego_distance_to_cut_in_vehicle_at_change_lane_end` | Cross of the duration of the lane change phase with the relative distance between the Ego and the cut-in vehicle at end of phase_essence_change_lane | cut_in_duration, ego_distance_to_cut_in_vehicle_at_change_lane_end
`cross_ego_distance_to_cut_in_vehicle_at_change_lane_end_ego_speed_at_change_lane_end` | Cross of the Ego distance to cut_in_vehicle and Ego speed at end | ego_distance_to_cut_in_vehicle_at_change_lane_end, ego_speed_at_change_lane_end

</details>

<details markdown="1">

<summary>[Click] The cross coverage items inherited from the <b>sut.generic_base_scenario</b> scenario are as follows:</summary>

Item | Description | Referred coverage items
-- | -- | -- 
`cross_ego_speed_on_curve_road_element_min_road_element_radius` | Cross cover of Ego's speed on curved road and road radius | ego_speed_on_curve_road_element, min_road_element_radius
`cross_min_road_element_radius_curve_road_direction` | Cross cover of curved road direction and road radius | min_road_element_radius, curve_road_direction

</details>

[//]: # ($$cross_coverage)


### KPI
The key performance indicators are given below.

#### Record items
The performance metrics and the data items captured during the test execution are as follows:

[//]: # ($$kpis)

Item | Description | Range | Unit/Type
-- | -- | -- | --
-- | -- | -- | --

<details markdown="1">

<summary>[Click] The KPIs inherited from the <b>sut.vehicle_cut_in_common</b> scenario are as follows:</summary>

Item | Description | Range | Unit/Type
-- | -- | -- | --
`cut_in_vehicle_length` | Length of the cut_in_vehicle |  | m
`cut_in_vehicle_width` | Width of the cut_in_vehicle |  | m
`cut_in_vehicle_height` | Height of the cut_in_vehicle |  | m
`ego_changed_lane` | Did the Ego change lane | true, false | bool

</details>

<details markdown="1">

<summary>[Click] The KPIs inherited from the <b>sut.generic_base_scenario</b> scenario are as follows:</summary>

Item | Description | Range | Unit/Type
-- | -- | -- | --
`ego_speed_at_end` | Actual speed of the Ego at the end of the scenario | [0..150), every: 10.0 | kph
`ego_avg_lon_acceleration` | Average longitudinal acceleration of the Ego throughout the scenario | [-3..2), every: 1.0 | mpsps
`ego_max_lat_acceleration` | The maximum absolute lateral acceleration of the Ego | [0..5), every: 1.0 | mpsps
`ego_max_lon_acceleration` | The maximum longitudinal acceleration of the Ego | [0..20), every: 1.0 | mpsps
`ego_min_lon_lane_distance` | The minimal longitudinal distance between the Ego and any actor in the lane coordinate system | [0..2), every: 0.2 | m
`ego_min_lat_lane_distance` | The minimal lateral distance between the Ego and any actor in the lane coordinate system | [0..2), every: 0.2 | m
`ego_min_euclidean_distance` | The minimal euclidean distance between the Ego and any actor | [0..200), every: 20.0 | m
`ego_min_ttc` | The minimal TTC between the Ego and any actor | [0..6), every: 0.5 | s
`ego_min_thw` | The minimal THW between the Ego and any actor | [0..31), every: 1.0 | s
`ego_collided` | Collision event between the Ego and any actor | true, false | bool
`min_road_element_curvature` | Minimum curvature of the road |  | float
`max_road_element_curvature` | Maximum curvature of the road |  | float
`ego_min_lon_acceleration` | The minimum longitudinal acceleration of the Ego | [-10..0), every: 1.0 | mpsps
`road_curvature_raw_value` | Raw value of road curvature |  | m
`ego_collision_velocity` | Collision velocity at the time of the collision between the Ego and any actor in the event of a collision | [2..14), every: 5.0 | kph
`ego_side_of_collision` | Side of Ego on which collision occured | front, front_left, left, back_left, back, back_right, right, front_right, other | av_car_side
`ego_min_speed_at_possible_collision` | Ego minimum speed at possible collision | [0..150), every: 10.0 | kph
`ego_max_speed_at_possible_collision` | Ego maximum speed at possible collision | [0..150), every: 10.0 | kph
`ego_min_acceleration_at_possible_collision` | Ego minimum acceleration at possible collision | [-10..0), every: 1.0 | mpsps
`ego_max_acceleration_at_possible_collision` | Ego maximum acceleration at possible collision | [0..20), every: 1.0 | mpsps
`ego_ttc_at_possible_collision` | Ego's TTC at possible collision in(s) |  | s

</details>

[//]: # ($$kpis)

[//]: # ($$metrics)



## Events

See common events [here](../vehicle_cut_in_common/base_vehicle_cut_in_common.md#events).

### Checks

|Default severity|Description|Issue kind|Threshold|
|---|--|---|---|
|`error	`|The cut_in_vehicle did not maintain its initial lane after aborted the cut-in maneuver. |cut_in_vehicle_did_not_maintain_initial_lane_after_aborted_cut_in| |




