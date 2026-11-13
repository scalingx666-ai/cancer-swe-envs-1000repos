# Issue

**Title:** Enhance xml import utility

## Description

Enhancements to XML import: Color parsing, polyline handling, independent annotations, and bounding boxes

## Summary

-Color Representation Fix:
The line color in the XML annotation is now correctly parsed from a decimal representation to a hexadecimal format.

-Handling Polyline vs. Polygon:
The XML import utility now differentiates between Polyline and polygons.
Now, if the region type is Polyline, it is correctly mapped to a LineString, while Polygon regions remain unchanged.

-Independent Annotation Groups:
Each XML annotation group is now processed as a separate annotation object.

-Bounding Box Implementation:
The bounding box is calculated as the smallest enclosing rectangle around the annotation, using the min/max X and Y coordinates.

The videos demonstrating the changes are below :

**Before:**

https://github.com/user-attachments/assets/8dd03562-a8c0-473f-921f-a5cb197aba10

**After:**

https://github.com/user-attachments/assets/75e44190-eefc-45b9-b2c9-d38761b95662


## Motivation
This PR improves the XML import utility by addressing multiple issues outlined in .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `eb5dcee2937a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.