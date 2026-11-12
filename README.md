# Lane-Crossing Labels

Labels created for 3 datasets and used in our paper *Detecting Lane Changes and Solid-Line Violations of Surrounding Vehicles From a Moving Camera Using Wheel-Road Contact Points*. B. Doğan and Ç. B. Erdaş. Submitted to IEEE TITS.

These are only labels. You will need to get the images from Argoverse 2, PREVENTION and Mapillary Vistas v2.0. Make sure to follow the rules of those datasets. All coordinates are pixel values of the original image.

## Files

`av2_crossings.csv` has 208 entries of vehicles crossing lane lines in Argoverse 2 Sensor front camera (ring_front_center, size 1550 x 2048).

| Column | Description |
|---|---|
| `split`, `log_id` | AV2 split (train/val) and log id |
| `frame_index`, `timestamp_ns` | Frame index (starting at 0) and timestamp of that frame in the log |
| `x_px`, `y_px` | Coordinates of a point on the vehicle (middle of the back bumper) while it's over the line it crossed |
| `line_type` | Solid or dashed line |
| `direction` | Left or right. Direction the vehicle crossed |
| `end_of_log` | There are 4 labels that occur in the last 0.4 seconds of a log. They are marked as True and won't be scored. |

`av2_logs.csv` contains all the logs we fully labelled. 700 logs from train split and 150 logs from val. Contains the number of `frames` and the `first_timestamp_ns` and `last_timestamp_ns` of each log. If a log here has no row in `av2_crossings.csv`, it doesn't contain any crossing.

`prevention_line_types.csv` contains the line types for each lane change in PREVENTION.

| Column | Description |
|---|---|
| `record`, `drive`, `vehicle_id` | Record id, drive and vehicle from PREVENTION |
| `lane_change_type` | Type of lane change in PREVENTION. 3 is left and 4 is right. 5 and 6 are other events and won't be scored. |
| `f0`, `f1`, `f2` | Start, crossing and ending frame of the lane change. f0 can be -1 if there is no starting frame. |
| `line_type` | Solid, dashed or no_event |

`vistas_vehicle_boxes.csv` has boxes around the instance polygons of the 7 vehicle classes of Mapillary Vistas v2.0. `class` column will say if it's `rear` (looking at the back of the vehicle) or `front` (everything else). It has the following columns. `split`, `image_id`, `image_width`, `image_height`, `box_index`, `class`, `x1`, `y1`, `x2`, `y2`

`vistas_contact_points.csv` has contact points for all the `rear` boxes. Join with `vistas_vehicle_boxes.csv` using `split`, `image_id` and `box_index`. These are the points where the outside edges of the rear tires touch the road. `left_x`, `left_y` are the left contact point. `right_x`, `right_y` are the right contact point. There may be empty values.

## License

CC BY-NC-SA 4.0. See LICENSE file. Same license as the original datasets.

## Citation

Please cite the paper above if you use these labels. Will add reference when published.
