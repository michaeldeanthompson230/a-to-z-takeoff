# A-Z Takeoff

## Software Requirements Specification (SRS)

Version: 0.1
Status: Draft
Author: Michael Thompson
Project: A-Z Takeoff

---

# 1. Project Overview

A-Z Takeoff is an AI-assisted construction takeoff and estimating platform designed to automatically convert residential construction plan PDFs into complete material packages and quote-ready bills of material.

Unlike traditional takeoff software that focuses primarily on measurements, A-Z Takeoff focuses on generating complete lumber-yard-quality estimates.

The software shall be capable of analyzing residential permit sets and converting construction drawings into material lists suitable for lumber yards, contractors, builders, and estimators.

---

# 2. Project Goals

The primary goal is to reduce the time required to create a complete construction material estimate.

The software shall:

* Read residential construction plans
* Detect walls and openings
* Interpret schedules and notes
* Generate complete framing packages
* Generate additional package takeoffs
* Produce customer-ready quote outputs

Long-term goal:

A user uploads a permit set PDF and receives a complete estimate with minimal manual input.

---

# 3. Target Users

Primary users include:

* Lumber yard estimators
* Building material suppliers
* General contractors
* Home builders
* Construction sales representatives

---

# 4. Platform Requirements

Initial platform:

* Windows Desktop Application
* Packaged as a standalone executable
* Local file processing
* Local database

Technology stack:

* Python
* PySide6
* OpenCV
* PyMuPDF
* SQLite
* Pandas

Future platform:

* Cloud application
* Multi-user support
* Shared pricing database
* CRM integration
* POS integration

---

# 5. Functional Requirements

The software shall:

1. Import PDF construction plans.
2. Classify plan sheets.
3. Detect drawing scales.
4. Detect wall geometry.
5. Detect openings.
6. Detect room labels.
7. Detect ceiling heights.
8. Read schedules.
9. Generate material quantities.
10. Generate customer quotes.

---

# 6. Plan Reading Requirements

## 6.1 PDF Import

The system shall accept:

* Single-page PDFs
* Multi-page PDFs
* Full permit sets

## 6.2 Sheet Classification

The software shall identify:

* Cover Sheets
* Site Plans
* Foundation Plans
* Floor Plans
* Roof Plans
* Roof Framing Plans
* Exterior Elevations
* Sections
* Details
* Electrical Plans
* Door Schedules
* Window Schedules

## 6.3 Scale Detection

The software shall detect scales automatically when available.

Examples:

* 1/4" = 1'-0"
* 3/16" = 1'-0"
* 1" = 8'

If scale cannot be determined, the sheet shall be flagged for review.

---

# 7. Wall Detection Requirements

## Exterior Walls

The software shall:

* Detect exterior wall geometry
* Measure wall lengths
* Detect wall thickness
* Classify wall type

Default assumptions:

* Exterior walls are 2x6 unless otherwise indicated
* Stud spacing per plan
* Default 16" O.C.

## Interior Walls

The software shall:

* Detect interior wall geometry
* Detect wall thickness
* Classify wall type

Default assumptions:

* Thin walls = 2x4
* Thick walls = 2x6
* Wet walls default to 2x6

## Visual Review Overlay

The software shall generate a review overlay.

Color Legend:

* Red = 2x6 wall assembly
* Blue = 2x4 wall assembly
* Yellow = Review required
* Green = Opening detected

The user shall be able to review and correct detected geometry.

---

# 8. Opening Detection Requirements

The software shall detect:

* Windows
* Doors
* Garage doors
* Sliding glass doors
* Bifold doors
* Barn doors

The software shall prioritize schedule information over graphical assumptions.

---

# 9. Framing Package Requirements

The framing package shall include:

## Foundation

* Anchor bolts
* PT sill plates
* Sill seal
* Hold-down hardware

## Wall Framing

* Studs
* Plates
* Headers
* Blocking
* Bracing

## Engineered Lumber

* LVLs
* I-joists
* Floor trusses
* Roof trusses
* Rim board

Only when called out on plans.

## Sheathing

* Wall sheathing
* Roof sheathing

## Weather Barrier

* Housewrap
* Flashing
* Tape

## Fasteners

* Framing nails
* Structural fasteners

## Connectors

* Simpson hardware
* Hangers
* Straps
* Hurricane ties

---

# 10. Estimating Rules

## Exterior Walls

* Double top plate
* Single bottom plate
* 10% framing waste
* 10% sheathing waste

## Interior Walls

* Double top plate
* Single bottom plate
* 10% framing waste

## Headers

Priority:

1. Plan callout
2. Beam schedule
3. LVL schedule
4. Default double 2x12 #2 SYP

Flag for review:

* Garage doors
* Structural openings
* Openings greater than 6 feet
* Large sliders

## Sheathing

Default wall sheathing:

* 7/16 OSB

## Housewrap

Default:

* 9' x 150' rolls

## Fasteners

Framing and sheathing:

* 2½" .131 electrogalvanized ring-shank coil framing nails

---

# 11. Material Database Requirements

The software shall maintain a material database.

Supported material categories:

* Dimensional lumber
* Pressure treated lumber
* Engineered lumber
* Sheathing
* Housewrap
* Fasteners
* Hardware

Future support:

* Vendor pricing
* Customer pricing
* Margin calculations

---

# 12. Quote Engine Requirements

The software shall generate:

## Internal Estimate

Includes:

* Material descriptions
* Quantities
* Waste calculations
* Review flags

## Customer Quote

Includes:

* Clean descriptions
* Pricing
* Package totals

---

# 13. Output Formats

The software shall support:

* PDF
* Excel
* CSV
* Printable quote
* Bill of Materials

---

# 14. Review Flags

The software shall flag:

* Missing scale
* Unclear wall type
* Unclear ceiling height
* Large openings
* Missing beam information
* Missing truss information
* Unrecognized plan notes

---

# 15. Future Modules

Future modules shall include:

## Exterior Package

* Siding
* Soffit
* Fascia
* Exterior trim

## Interior Package

* Drywall
* Baseboard
* Casing
* Crown molding

## Openings Package

* Windows
* Doors
* Hardware

## Millwork Package

* Cabinets
* Countertops

## Roofing Package

* Shingles
* Metal roofing
* Underlayment
* Flashing

## Pricing Module

* Vendor pricing
* Margin engine
* Quote builder

## Enterprise Features

* Multi-user support
* User permissions
* Cloud synchronization
* CRM integration
* POS integration

---

# 16. Success Criteria

Version 1.0 shall be considered successful when:

* A user uploads a residential permit set.
* The software automatically identifies wall geometry.
* The software generates a framing package.
* The estimate is sufficiently accurate for rapid estimator review.

Target accuracy:

* Wall lengths within 5%
* Stud counts within 10%
* Sheathing quantities within 10%
* Opening detection substantially correct
* Major structural components identified correctly

The final objective is to reduce estimating time from hours to minutes while maintaining lumber-yard-quality estimates.
