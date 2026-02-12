# Test Cases: Inland Marine & E&O Coverage Upload

## Overview
Test cases for validating the upload and mapping of 16 Inland Marine and E&O coverages to ZIP system.


## Inland Marine Coverage Test Cases

### TC-IM-001: L07 Bailees Innkeepers Limit Upload
**Objective:** Verify L07 Bailees Innkeepers Limit is correctly uploaded to ZIP
- **Precondition:** User has valid Inland Marine policy data
- **Steps:**
  1. Navigate to upload staging tab
  2. Enter L07 Bailees Innkeepers Limit value (e.g., $100,000)
  3. Click Upload to ZIP
- **Expected Result:** Coverage maps correctly and appears in ZIP system
- **Data:** Limit value transfers without loss or corruption

### TC-IM-002: L07 Bailees Innkeepers Deductible Upload
**Objective:** Verify L07 Bailees Innkeepers Deductible mapping
- **Precondition:** L07 Bailees Innkeepers Limit already configured
- **Steps:**
  1. Enter L07 Bailees Innkeepers Ded value (e.g., $5,000)
  2. Submit to ZIP
- **Expected Result:** Deductible maps to correct field in ZIP
- **Validation:** Ded ≤ Limit

### TC-IM-003: L07 Bailees Innkeepers Premium Upload
**Objective:** Verify L07 Bailees Innkeepers Premium calculation and upload
- **Precondition:** Limit and Deductible configured
- **Steps:**
  1. Enter Premium value
  2. Verify calculation is correct
  3. Upload to ZIP
- **Expected Result:** Premium displays in ZIP with correct formatting
- **Data Type:** Numeric with 2 decimal places

### TC-IM-004: 668 Bailees Innkeepers Per Occurrence Limit Upload
**Objective:** Verify per occurrence limit mapping for code 668
- **Precondition:** General Bailees Innkeepers coverage active
- **Steps:**
  1. Enter 668 per occ limit (e.g., $50,000)
  2. Upload to ZIP
- **Expected Result:** Per occurrence limit appears in ZIP
- **Validation:** Per occ limit ≤ Aggregate limit

### TC-IM-005: 668 Bailees Innkeepers Per Occurrence Deductible Upload
**Objective:** Verify per occurrence deductible for code 668
- **Precondition:** Per occurrence limit configured
- **Steps:**
  1. Enter 668 deductible value
  2. Submit to ZIP
- **Expected Result:** Deductible correctly mapped and stored
- **Validation:** Per occ ded ≤ Per occ limit

### TC-IM-006: 665 Bailees Innkeepers Per Guest Limit Upload
**Objective:** Verify per guest limit mapping for code 665
- **Precondition:** Bailees Customers policy active
- **Steps:**
  1. Enter 665 per guest limit (e.g., $25,000)
  2. Upload to ZIP
- **Expected Result:** Per guest limit displays correctly in ZIP
- **Validation:** Per guest limit ≤ Per occurrence limit

### TC-IM-007: 665 Bailees Innkeepers Per Guest Deductible Upload
**Objective:** Verify per guest deductible for code 665
- **Precondition:** Per guest limit configured
- **Steps:**
  1. Enter 665 per guest deductible
  2. Submit to ZIP
- **Expected Result:** Deductible correctly stored with guest limit
- **Validation:** Per guest ded ≤ Per guest limit

### TC-IM-008: L11 Bailees Customers Limit Upload
**Objective:** Verify L11 Bailees Customers limit mapping
- **Precondition:** Customers coverage enabled
- **Steps:**
  1. Enter L11 limit value (e.g., $75,000)
  2. Upload to ZIP
- **Expected Result:** Limit correctly mapped to ZIP
- **Data Integrity:** No truncation or rounding

### TC-IM-009: L11 Bailees Customers Deductible Upload
**Objective:** Verify L11 Bailees Customers deductible mapping
- **Precondition:** L11 limit configured
- **Steps:**
  1. Enter L11 deductible value
  2. Submit to ZIP
- **Expected Result:** Deductible appears with correct association
- **Validation:** Ded ≤ Limit

### TC-IM-010: L11 Bailees Customers Premium Upload
**Objective:** Verify L11 Bailees Customers premium calculation
- **Precondition:** Limit and Deductible configured
- **Steps:**
  1. Verify premium calculation
  2. Upload to ZIP
- **Expected Result:** Premium displays with correct decimal formatting
- **Data Type:** Currency format (2 decimals)

---

## E&O Coverage Test Cases

### TC-EO-001: Specialties Policy Type Upload
**Objective:** Verify Specialties Policy Type field is correctly mapped
- **Precondition:** E&O coverage section accessible
- **Steps:**
  1. Select Specialties Policy Type (e.g., "Miscellaneous" or "Professional")
  2. Upload to ZIP
- **Expected Result:** Policy Type correctly stored in ZIP
- **Validation:** Field contains valid enumerated value

### TC-EO-002: Claims Made Indicator Upload
**Objective:** Verify Claims Made Indicator flag is correctly set
- **Precondition:** Specialties Policy Type configured
- **Steps:**
  1. Toggle Claims Made Indicator (Yes/No)
  2. Upload to ZIP
- **Expected Result:** Indicator correctly reflects in ZIP
- **Valid Values:** True/False or Yes/No

### TC-EO-003: Specialties E&O Miscellaneous E&O Limit Upload
**Objective:** Verify E&O Miscellaneous limit mapping
- **Precondition:** E&O coverage active with Claims Made Indicator set
- **Steps:**
  1. Enter Miscellaneous E&O Limit (e.g., $1,000,000)
  2. Upload to ZIP
- **Expected Result:** Limit correctly mapped and stored
- **Data Integrity:** Full amount preserved

### TC-EO-004: Specialties E&O Miscellaneous E&O Deductible Upload
**Objective:** Verify E&O Miscellaneous deductible mapping
- **Precondition:** Miscellaneous Limit configured
- **Steps:**
  1. Enter Miscellaneous E&O Deductible (e.g., $25,000)
  2. Submit to ZIP
- **Expected Result:** Deductible correctly associated with limit
- **Validation:** Ded ≤ Limit

### TC-EO-005: Specialties E&O Miscellaneous E&O Premium Upload
**Objective:** Verify E&O Miscellaneous premium calculation
- **Precondition:** Limit and Deductible configured
- **Steps:**
  1. Verify premium calculation
  2. Upload to ZIP
- **Expected Result:** Premium displays with correct formatting
- **Data Type:** Numeric with 2 decimal places

---

## Reinsurance Commission Test Cases

### TC-RC-001: Reinsurance Commission % Upload
**Objective:** Verify Reinsurance Commission percentage is correctly mapped
- **Precondition:** Reinsurance section active
- **Steps:**
  1. Enter Reinsurance Commission % (e.g., 15.5)
  2. Upload to ZIP
- **Expected Result:** Commission % correctly stored in ZIP
- **Validation:** Value is between 0-100%

### TC-RC-002: Reinsurance Commission % Calculation
**Objective:** Verify Commission % is used in premium calculations
- **Precondition:** Commission % configured
- **Steps:**
  1. Calculate expected reinsurance commission
  2. Verify calculation with uploaded value
- **Expected Result:** Commission amount correctly calculated
- **Formula Validation:** Commission = Premium × (Commission % / 100)

---

## Integration Test Cases

### TC-INT-001: All 16 Coverages Bulk Upload
**Objective:** Verify all coverages upload together without conflicts
- **Precondition:** All coverage fields populated with valid data
- **Steps:**
  1. Fill in all 16 coverage fields in staging tab
  2. Click "Upload All to ZIP"
  3. Verify completion status
- **Expected Result:** All 16 coverages successfully mapped to ZIP
- **Validation:** No missing or orphaned records

### TC-INT-002: Partial Coverages Upload
**Objective:** Verify subset of coverages can be uploaded
- **Precondition:** 5 coverage fields populated
- **Steps:**
  1. Select specific coverages to upload
  2. Submit selection
- **Expected Result:** Only selected coverages upload; others remain in staging
- **Data Consistency:** Uploaded and staging-only coverages don't conflict

### TC-INT-003: Duplicate Coverage Prevention
**Objective:** Verify system prevents duplicate coverage uploads
- **Precondition:** Coverage already uploaded to ZIP
- **Steps:**
  1. Attempt to re-upload same coverage
  2. Observe system response
- **Expected Result:** System prevents duplicate or updates existing record
- **Message:** Clear message to user about duplicate attempt

---

## Error & Validation Test Cases

### TC-ERR-001: Invalid Limit Value
**Objective:** Verify system rejects invalid limit values
- **Precondition:** Upload form open
- **Steps:**
  1. Enter negative or non-numeric limit value
  2. Attempt upload
- **Expected Result:** Validation error displays
- **Message:** Clear error indicating valid format required

### TC-ERR-002: Deductible Exceeds Limit
**Objective:** Verify system validates deductible ≤ limit
- **Precondition:** Coverage limit set to $50,000
- **Steps:**
  1. Enter deductible of $75,000
  2. Attempt upload
- **Expected Result:** Validation error prevents upload
- **Message:** "Deductible cannot exceed limit"

### TC-ERR-003: Commission % Out of Range
**Objective:** Verify commission percentage must be 0-100
- **Precondition:** Reinsurance section open
- **Steps:**
  1. Enter Commission % of 150
  2. Attempt upload
- **Expected Result:** Validation error prevents upload
- **Message:** "Commission % must be between 0 and 100"

### TC-ERR-004: Missing Required Coverage Fields
**Objective:** Verify required fields are enforced
- **Precondition:** Form ready for submission
- **Steps:**
  1. Leave Specialties Policy Type blank
  2. Attempt upload
- **Expected Result:** Upload blocked with error
- **Message:** "Specialties Policy Type is required"

---

## Data Mapping Verification Test Cases

### TC-DM-001: Inland Marine to ZIP Field Mapping
**Objective:** Verify each Inland Marine coverage maps to correct ZIP field
- **Precondition:** ZIP system field documentation available
- **Steps:**
  1. Map each coverage to expected ZIP field
  2. Verify no field conflicts
- **Expected Result:** Each coverage maps to unique, correct ZIP field
- **Documentation:** Cross-reference ZIP data model

### TC-DM-002: E&O to ZIP Field Mapping
**Objective:** Verify each E&O coverage maps to correct ZIP field
- **Precondition:** ZIP system field documentation available
- **Steps:**
  1. Verify Specialties Policy Type mapping
  2. Verify Claims Made Indicator mapping
  3. Verify Miscellaneous E&O limit/ded/premium mappings
- **Expected Result:** All E&O coverages correctly mapped
- **Data Model:** Consistent with ZIP schema

### TC-DM-003: Data Type Consistency
**Objective:** Verify all uploaded data matches expected ZIP data types
- **Precondition:** Data types documented for each field
- **Steps:**
  1. Upload currency fields (should be decimal)
  2. Upload boolean fields (should be true/false)
  3. Upload text fields (should be string)
- **Expected Result:** Data types preserved in ZIP
- **Validation:** No type conversion errors

---

## Performance & Load Test Cases

### TC-PERF-001: Single Coverage Upload Performance
**Objective:** Verify single coverage uploads in reasonable time
- **Precondition:** Network connection stable
- **Steps:**
  1. Upload one coverage
  2. Measure upload time
- **Expected Result:** Upload completes within 5 seconds
- **Threshold:** Acceptable latency ≤ 5 seconds

### TC-PERF-002: Bulk 16 Coverage Upload Performance
**Objective:** Verify all 16 coverages upload efficiently
- **Precondition:** All fields populated
- **Steps:**
  1. Upload all 16 coverages together
  2. Measure total time
  3. Verify ZIP system receives all data
- **Expected Result:** Bulk upload completes within 10 seconds
- **Data Integrity:** All records received without loss

---

## User Experience Test Cases

### TC-UX-001: Staging Tab Display
**Objective:** Verify all 16 coverages visible and organized in staging tab
- **Precondition:** Upload staging tab open
- **Steps:**
  1. Review staging tab layout
  2. Verify all 16 coverages are listed
  3. Check grouping (Inland Marine, E&O, Reinsurance)
- **Expected Result:** All coverages clearly visible and organized
- **Layout:** Logical grouping by coverage type

### TC-UX-002: Clear Upload Confirmation
**Objective:** Verify user receives confirmation after successful upload
- **Precondition:** Coverages uploaded to ZIP
- **Steps:**
  1. Complete upload process
  2. Observe confirmation message
- **Expected Result:** Clear success message displays
- **Information:** Shows number of coverages uploaded

---

## Summary

**Total Test Cases:** 31
- **Inland Marine:** 10 test cases
- **E&O:** 5 test cases  
- **Reinsurance:** 2 test cases
- **Integration:** 3 test cases
- **Error & Validation:** 4 test cases
- **Data Mapping:** 3 test cases
- **Performance:** 2 test cases
- **User Experience:** 2 test cases