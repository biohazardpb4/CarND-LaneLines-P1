# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

// names=$(ls | sed s/[0-9]//g | uniq);for fn in $names; do echo ["$fn"]: "./test_images_output/$fn"001 '"Color"'; done
// names=$(ls | sed s/[0-9]//g | uniq);for fn in $names; do echo ![alt text]["$fn"]; done

[canny_region_merged_color_selection_white_selected_challenge-]: ./test_images_output/canny_region_merged_color_selection_white_selected_challenge-010 "Color"
[merged_color_selection_white_selected_challenge-]: ./test_images_output/merged_color_selection_white_selected_challenge-010 "Color"
[region_merged_color_selection_white_selected_challenge-]: ./test_images_output/region_merged_color_selection_white_selected_challenge-010 "Color"
[two_lane_region_merged_color_selection_white_selected_challenge-]: ./test_images_output/two_lane_region_merged_color_selection_white_selected_challenge-010 "Color"
[white_selected_challenge-]: ./test_images_output/white_selected_challenge-010 "Color"
[with_lanes_region_merged_color_selection_white_selected_challenge-]: ./test_images_output/with_lanes_region_merged_color_selection_white_selected_challenge-010 "Color"
[yellow_selected_challenge-]: ./test_images_output/yellow_selected_challenge-010 "Color"


---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps:
1. Select white lanes

   ![alt text][white_selected_challenge-]

1. Select yellow lanes
   
   ![alt text][yellow_selected_challenge-]

1. Merge white and yellow lane selections

   ![alt text][merged_color_selection_white_selected_challenge-]
   
1. Select lane region triangle

   ![alt text][region_merged_color_selection_white_selected_challenge-]
   
1. Find edges via Canny

   ![alt text][canny_region_merged_color_selection_white_selected_challenge-]
   
1. Extract lanes via Hough

   ![alt text][two_lane_region_merged_color_selection_white_selected_challenge-]

1. Split into two groups based on slope sign, and average each group's slopes and x intercepts

   ![alt text][with_lanes_region_merged_color_selection_white_selected_challenge-]

In order to draw a single line on the left and right lanes, I modified the last step of the pipeline to split into two groups based on slope sign, and average each group's slopes and x intercepts.


### 2. Identify potential shortcomings with your current pipeline


1. I think that the white lane selection could be better tuned.
1. I think that we may be able to select regions of the left and right lane individually, but we likely risk overfitting.
1. Lines that we know are bad are not thrown out of the Hough transform output.
1. We only fit lines, not curves.
1. The parameters are hand tuned.


### 3. Suggest possible improvements to your pipeline

1. I could use the interactive color filter tuner to determine tighter bounds on what filters to set for the white line selection.
1. We could select lane regions individually to prevent lane crossover.
1. We could make better slope buckets and only include lines from Hough that fit into the filtered buckets.
1. We could use the generalized Hough transform to infer lanes that curve.
1. We could tune parameters more automatically by telling an algorithm to maximize the area of interest kept and minimize the region of interest that's filtered.
