ID	                Requirement	                                Priority
FR-01	Users can enter RA and Dec	                                Critical
FR-02	Users can search SPHEREx observations	                        Critical
FR-03	Users can retrieve actual astronomical images	                Critical
FR-04	Users can view observations chronologically	                Critical
FR-05	Users can animate observations	                                Critical
FR-06	Users can compare two images	                                High
FR-07	Users can generate difference images	                        High
FR-08	Users can view data-quality information	                        High
FR-09	Users can inspect spectral channels	                        Medium
FR-10	Users can identify detected sources	                        Medium
FR-11	Users can overlay external catalogs	                        Medium
FR-12	Users can submit candidate observations	                        Future

# SPHEREx Temporal Explorer
## Software Requirements Specification (SRS)

**Project Name:** SPHEREx Temporal Explorer  
**Document Type:** Software Requirements Specification  
**Version:** 1.0  
**Status:** Initial Development Specification

---

## 1. Introduction

### 1.1 Purpose

This document defines the functional and non-functional requirements of SPHEREx Temporal Explorer, a web-based astronomical data exploration platform designed to retrieve, visualize, and analyze multi-epoch observations from the Spectro-Photometer for the History of the Universe, Epoch of Reionization, and Ices Explorer (SPHEREx) mission.

The system aims to provide users with an accessible interface for investigating astronomical objects and regions of the sky through coordinate-based searches, chronological image visualization, multi-epoch comparisons, and basic astronomical data analysis.

### 1.2 Scope

SPHEREx Temporal Explorer will allow users to specify celestial coordinates, search available SPHEREx observations, retrieve actual astronomical image products, and examine observations across different epochs.

The platform will initially prioritize image retrieval and temporal visualization. Additional capabilities will include image comparison, difference imaging, data-quality inspection, spectral-channel exploration, source detection, and external catalog integration.

The system will use publicly available astronomical datasets and archive services. The availability of individual observations and scientific products will depend on the data exposed by the SPHEREx archive.

### 1.3 Intended Users

- Astronomy enthusiasts and students.
- Researchers and amateur astronomers.
- Computer science and data science students.
- Users interested in investigating astronomical variability and motion.

---

## 2. Functional Requirements

Functional requirements define the specific operations and capabilities that the system must provide.

### 2.1 Requirement Priority Classification

| Priority | Meaning |
|---|---|
| Critical | Essential for the minimum viable product (MVP). |
| High | Important for the primary application experience. |
| Medium | Additional functionality that improves analytical capabilities. |
| Future | Intended for a later development phase. |

### 2.2 Functional Requirements Specification

#### FR-01: Celestial Coordinate Input

**Priority:** Critical

**Description:**  
The system shall allow users to enter the Right Ascension (RA) and Declination (Dec) coordinates of an astronomical target.

**Expected Behavior:**
- Accept coordinates in decimal degrees.
- Support sexagesimal coordinate input where implemented.
- Validate RA within 0° to 360° and Dec within −90° to +90°.
- Reject invalid or incomplete coordinate entries.
- Allow users to specify a search field of view.

**Acceptance Criteria:**
- Users can successfully submit valid RA and Dec values.
- Invalid coordinates generate understandable validation messages.
- Valid coordinates are converted into a consistent internal representation before archive queries.

#### FR-02: SPHEREx Observation Search

**Priority:** Critical

**Description:**  
The system shall query available SPHEREx archive services to identify observations associated with the specified celestial coordinates and search region.

**Expected Behavior:**
- Submit coordinate-based queries to the relevant archive interface.
- Retrieve available observation metadata.
- Identify observation dates, product identifiers, and relevant spectral or instrumental metadata when available.
- Handle empty search results and archive communication failures.

**Acceptance Criteria:**
- The system returns available observations matching the search criteria.
- Observation metadata is displayed in a structured format.
- Users receive an informative message when no matching observations are available.

#### FR-03: Astronomical Image Retrieval

**Priority:** Critical

**Description:**  
The system shall retrieve actual astronomical image products associated with selected SPHEREx observations.

**Expected Behavior:**
- Retrieve image products from valid archive-provided locations.
- Read supported FITS astronomical data files.
- Extract the relevant image data and associated metadata.
- Preserve the original scientific data and its provenance.
- Handle unavailable, corrupted, or unsupported files.

**Acceptance Criteria:**
- At least one genuine SPHEREx astronomical image can be retrieved and displayed.
- Image metadata and source information are retained.
- Failed downloads or invalid FITS files produce appropriate error messages.

#### FR-04: Chronological Observation Visualization

**Priority:** Critical

**Description:**  
The system shall organize and display available observations according to their observation timestamps.

**Expected Behavior:**
- Extract observation timestamps from archive metadata or FITS headers.
- Sort observations chronologically.
- Display the corresponding observation date and relevant metadata.
- Allow users to select individual observations.

**Acceptance Criteria:**
- Observations appear in chronological order.
- Selecting an observation displays its corresponding astronomical image.
- The displayed timestamp corresponds to the selected observation's metadata.

#### FR-05: Temporal Image Animation

**Priority:** Critical

**Description:**  
The system shall provide an animation interface that allows users to visualize a sequence of astronomical observations over time.

**Expected Behavior:**
- Display selected observations as sequential image frames.
- Provide play and pause controls.
- Allow users to move between frames.
- Allow adjustment of animation speed.
- Display the observation timestamp associated with each frame.

**Acceptance Criteria:**
- Users can play and pause an observation sequence.
- Users can navigate individual frames.
- The displayed timestamps update with the corresponding frames.
- The animation preserves the chronological order of observations.

#### FR-06: Multi-Image Comparison

**Priority:** High

**Description:**  
The system shall allow users to select and visually compare two astronomical observations.

**Expected Behavior:**
- Allow selection of two observation products.
- Display the selected images side by side.
- Provide relevant observation metadata for both images.
- Support spatial alignment when necessary to enable meaningful comparison.

**Acceptance Criteria:**
- Users can select two available observations.
- Both images can be displayed simultaneously.
- The interface identifies the observation date and other relevant metadata for each image.
- When alignment is applied, the system provides the necessary common-coordinate representation.

#### FR-07: Difference Image Generation

**Priority:** High

**Description:**  
The system shall generate a difference image from two selected and appropriately aligned astronomical observations.

**Expected Behavior:**
- Use images with compatible scientific interpretation and coordinate alignment.
- Calculate pixel-wise differences between corresponding image locations.
- Preserve valid-pixel masks and account for unavailable coverage.
- Display the resulting difference image.
- Identify relevant processing information and limitations.

**Acceptance Criteria:**
- The system can generate a difference image from two compatible observations.
- Invalid or uncovered pixels are not incorrectly interpreted as valid measurements.
- The resulting image can be visualized through the application.
- The system identifies the two input observations used to generate the result.

#### FR-08: Data-Quality Inspection

**Priority:** High

**Description:**  
The system shall provide access to available data-quality information associated with retrieved astronomical observations.

**Expected Behavior:**
- Display available quality flags and masks.
- Identify missing or invalid pixel regions.
- Display uncertainty or variance information when supplied by the selected data product.
- Present relevant calibration and processing metadata when available.

**Acceptance Criteria:**
- Users can inspect available data-quality information.
- Missing or invalid data regions can be distinguished from valid image pixels.
- The system does not fabricate quality information when the archive does not provide it.

#### FR-09: Spectral-Channel Inspection

**Priority:** Medium

**Description:**  
The system shall allow users to inspect available SPHEREx spectral-channel information associated with retrieved observations.

**Expected Behavior:**
- Identify available spectral-channel metadata.
- Display corresponding wavelength information when supplied by the data product.
- Allow users to select and inspect available channels.
- Present relevant channel information alongside the corresponding observation.

**Acceptance Criteria:**
- Available spectral-channel information can be displayed.
- Channel selection retrieves or displays the corresponding available data.
- Wavelength information is consistent with the underlying product metadata.

#### FR-10: Astronomical Source Detection

**Priority:** Medium

**Description:**  
The system shall provide a source-detection capability for identifying astronomical sources within selected image regions.

**Expected Behavior:**
- Apply an astronomical source-detection algorithm to suitable image data.
- Estimate detected source positions.
- Convert image coordinates into celestial coordinates using the image's WCS information.
- Display detected sources as markers or overlays.
- Provide available detection measurements and confidence information.

**Acceptance Criteria:**
- The system can identify candidate sources in a supported image.
- Detected positions can be represented in celestial coordinates.
- Detected sources can be visualized over the original image.
- Detection results include relevant measurements and algorithm parameters.

#### FR-11: External Astronomical Catalog Overlay

**Priority:** Medium

**Description:**  
The system shall support the retrieval and visualization of relevant external astronomical catalog data over SPHEREx images.

**Expected Behavior:**
- Query supported external astronomical catalogs.
- Retrieve relevant source coordinates and available metadata.
- Match catalog entries to the selected image region.
- Display catalog sources as overlays.
- Distinguish external catalog sources from detections generated by the application.

**Acceptance Criteria:**
- External catalog sources can be retrieved for a supported region.
- Catalog positions are correctly transformed into the image coordinate system.
- Catalog entries are distinguishable from application-generated detections.
- Catalog source information and provenance are available.

#### FR-12: Candidate Observation Submission

**Priority:** Future

**Description:**  
The system shall provide a mechanism for users to submit candidate astronomical observations or potentially interesting findings for further investigation.

**Expected Behavior:**
- Allow users to submit candidate coordinates and associated observation identifiers.
- Collect a description of the candidate finding.
- Validate submitted information.
- Store submissions for subsequent review.
- Provide submission status or confirmation.

**Acceptance Criteria:**
- Users can submit valid candidate information.
- Invalid submissions are rejected with understandable messages.
- Submitted candidates can be retrieved by authorized reviewers.
- Submission records retain relevant observation references and timestamps.

---

## 3. Non-Functional Requirements

Non-functional requirements define the quality attributes, operational constraints, and performance expectations of the system.

### NFR-01: Usability

The system shall provide an intuitive interface that allows users with basic astronomical knowledge to search and explore observations without requiring direct interaction with astronomical archive APIs.

### NFR-02: Performance

The system shall minimize unnecessary archive requests, use caching where appropriate, and process astronomical images efficiently. Image retrieval and processing times shall be measured during testing and optimized according to the available infrastructure.

### NFR-03: Reliability

The system shall handle archive failures, unavailable observations, invalid FITS files, and incomplete data without terminating the entire application.

### NFR-04: Data Integrity

The system shall preserve the integrity of original astronomical data and distinguish original measurements from processed, transformed, or visualization-only representations.

### NFR-05: Scientific Accuracy

Coordinate transformations, image alignment, difference calculations, and source measurements shall use appropriate astronomical libraries and scientifically valid procedures.

### NFR-06: Compatibility

The web application shall support modern desktop web browsers and provide a responsive interface for different screen sizes where practical.

### NFR-07: Maintainability

The software shall use modular components that separate archive access, astronomical data processing, backend services, database operations, and frontend visualization.

### NFR-08: Security

The system shall validate user inputs, protect backend services, manage credentials through environment variables, and prevent unauthorized access to restricted operations.

### NFR-09: Scalability

The architecture shall allow additional astronomical data sources, observation products, processing capabilities, and users to be supported without requiring a complete redesign.

### NFR-10: Traceability and Provenance

The system shall retain relevant information about the origin of astronomical observations and the processing steps applied to generated products.

---

## 4. System Constraints and Assumptions

1. The system depends on the availability and accessibility of SPHEREx data products through supported archive services.
2. Available observations, temporal coverage, spectral information, and quality metadata depend on the actual archive products.
3. The system shall not assume that every astronomical target has multiple usable observations.
4. Image comparison and difference imaging require compatible data and appropriate spatial alignment.
5. Source detection and photometric analysis depend on image quality, calibration, uncertainty information, and the suitability of the selected algorithm.
6. External catalog integration depends on the availability and terms of the selected catalog services.
7. Scientific outputs must distinguish measured results from estimates, predictions, and visualization transformations.

---

## 5. MVP Development Scope

The initial Minimum Viable Product shall prioritize the following requirements:

| Requirement | MVP Implementation |
|---|---|
| FR-01 | Coordinate input and validation |
| FR-02 | SPHEREx archive query |
| FR-03 | FITS retrieval and image extraction |
| FR-04 | Chronological observation display |
| FR-05 | Multi-epoch image animation |
| FR-06 | Two-image comparison |
| FR-07 | Basic difference image generation |
| FR-08 | Display available quality metadata |

FR-09 through FR-12 may be developed after the primary observation retrieval and temporal visualization workflow has been demonstrated successfully.

---

## 6. Requirement Traceability

Each functional requirement shall be associated with its corresponding implementation module and testing procedure.

| Requirement | Proposed Module | Verification Method |
|---|---|---|
| FR-01 | Coordinate Input / Validation | Input validation tests |
| FR-02 | Archive Query Service | Archive integration tests |
| FR-03 | FITS Reader / Image Retrieval | FITS retrieval and inspection tests |
| FR-04 | Observation Manager | Chronological sorting tests |
| FR-05 | Temporal Viewer | Interface and animation tests |
| FR-06 | Image Comparison | Visual comparison tests |
| FR-07 | Difference Imaging | Numerical and image validation |
| FR-08 | Quality Inspector | Metadata and mask validation |
| FR-09 | Spectral Inspector | Channel metadata tests |
| FR-10 | Source Detection | Detection and coordinate validation |
| FR-11 | Catalog Integration | Cross-catalog coordinate matching |
| FR-12 | Candidate Submission | Submission and database tests |

---

## 7. Document Maintenance

This document shall be updated as the system architecture, implementation scope, and technical understanding evolve.

Changes to requirements shall be documented with their corresponding requirement identifiers, priority levels, implementation status, and verification procedures.
