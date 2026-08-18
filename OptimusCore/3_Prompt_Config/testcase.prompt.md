# Prompts for User Case and Test Case Generation

## Section 1: User Case Generation Prompt

### Purpose
Generate comprehensive user stories with acceptance criteria for insurance policy management features in the ZIP system.

### Prompt Template

```
You are an expert insurance domain analyst specializing in ZIP policy management system requirements.

Generate a detailed user story based on the following information:

**Input Details:**
- Feature/Module: [FEATURE NAME]
- Business Requirement: [BUSINESS DESCRIPTION]
- Affected LOB/SBU: [LINE OF BUSINESS / STRATEGIC BUSINESS UNIT]
- Policy Type: [POLICY TYPE CODE AND NAME]
- Impact Area: [e.g., Locations, Coverages, Deductibles, Limits, Premiums]

**Output Requirements:**

Generate a user story in the following format:

### User Story: [CLEAR, CONCISE TITLE]

**As a** [USER ROLE - e.g., Underwriter, Admin, Policyholder]
**I want** [ACTION/CAPABILITY]
**So that** [BUSINESS VALUE/BENEFIT]

**Background:**
- [Business context and why this is needed]
- [Related policies, coverages, or modules affected]
- [Regulatory or compliance requirements if applicable]

**Acceptance Criteria:**
1. [Specific, verifiable acceptance criterion]
2. [Specific, verifiable acceptance criterion]
3. [Specific, verifiable acceptance criterion]
4. [Validation rules and constraints]
5. [Error handling scenarios]
6. [Data integrity requirements]

**Technical Considerations:**
- [Database tables affected]
- [Integration points with other systems]
- [Performance requirements]
- [Security/Authorization requirements]

**Business Rules:**
- [Business rule 1]
- [Business rule 2]
- [Business rule 3]

**Out of Scope:**
- [What is explicitly NOT included]
- [Related features to be handled separately]

**Dependencies:**
- [Other user stories or features that must be completed first]
```

### Usage Example

**Input:**
```
Feature/Module: Accident & Health Location Management
Business Requirement: Add support for Out of Country locations (non-Canadian) without provincial coding
Affected LOB/SBU: 057 / SP Specialties
Policy Type: AH Accident & Health
Impact Area: Locations section, Country coding
```

**Expected Output:** (See Section 1A below)

---

## Section 1A: User Story Template - Out of Country Location

### User Story: Create Out of Country Location for Non-Canadian Insureds

**As an** Underwriter managing Accident & Health policies
**I want** to create policy locations for out-of-country insureds that are not tied to Canadian provinces
**So that** we can write policies for non-resident customers without applying incorrect provincial tax

**Background:**
- Current system requires all locations to be mapped to Canadian provinces
- This creates incorrect tax calculations for out-of-country customers
- Business needs to support 12+ provinces PLUS out-of-country option
- Non-residents should have zero tax on premiums

**Acceptance Criteria:**
1. On the "Work with Location" screen, F9 add function must allow creation of new locations
2. On "Maintain Location" screen, a new country code "OOC" (Out of Canada) must be available for selection
3. When OOC is selected, the following fields must auto-populate:
   - Address field: "Out of Canada - A&H only"
   - City field: "Out of Canada - A&H only"
4. When OOC is selected, Province and Postal Code fields must be hidden or disabled
5. System must auto-populate Cresta Zone, Windstorm Zone, and Flood Zone as blank (not required)
6. System must prevent creation of more than ONE out-of-country location per policy
7. Other province-based locations must still be creatable alongside the single OOC location
8. All existing coverages must automatically apply to the OOC location
9. Tax calculation must result in $0 tax for OOC locations
10. System must validate data integrity between ZIP and ClaimsCentre for OOC locations

**Technical Considerations:**
- Database: Update Location Master table with OOC country code
- Integration: ClaimsCentre mapping must support OOC for all coverage claim questions (BI, FL, MP, PD, PI, BD)
- Performance: No impact to existing location queries
- Security: Underwriters must have authorization to use OOC code

**Business Rules:**
- Only ONE out-of-country location per policy
- OOC location cannot be combined with single-province locations
- OOC locations inherit all policy coverages without modification
- Tax rate for OOC = 0%
- ClaimsCentre must recognize OOC for all claim mapping questions

**Out of Scope:**
- Changes to coverage definitions
- Module changes (Accident & Sickness remains unchanged)
- ClaimsCentre development (separate coordination)

**Dependencies:**
- ClaimsCentre OOC mapping configuration
- Confirmation of tax calculation rules with Finance

---

## Section 2: Test Case Generation Prompt

### Purpose
Generate comprehensive test cases for validating user stories and features in the ZIP insurance system.

### Prompt Template

```
You are an expert QA analyst specializing in insurance policy management systems.

Generate comprehensive test cases based on the following user story:

**Input Details:**
- User Story: [USER STORY TITLE]
- Feature: [FEATURE NAME]
- Acceptance Criteria: [LIST OF 5-10 ACCEPTANCE CRITERIA]
- Coverage Types: [e.g., Bailees Innkeepers, Medical Payments, Bodily Injury]
- Data Types: [e.g., Currency, Numeric with decimals, Date, Text]
- System: [e.g., ZIP Policy Management]

**Output Requirements:**

Generate a comprehensive test case suite with:
1. At least 10 test cases covering:
   - Positive scenarios (happy path)
   - Negative scenarios (error handling)
   - Boundary conditions
   - Data validation
   - Business rule validation
   - Integration points

**Format for Each Test Case:**

### TC-[CODE]-[NUMBER]: [DESCRIPTIVE TITLE]

**Objective:**
[Clear statement of what is being tested]

**Preconditions:**
- [System state before test execution]
- [Required data setup]
- [Required access/permissions]

**Test Data:**
- [Specific values to use in the test]
- [Any dependent data]

**Steps:**
1. [Action 1]
2. [Action 2]
3. [Action 3]
4. [Assertion/Validation step]

**Expected Result:**
[Specific, verifiable expected outcome]

**Actual Result:**
[To be filled during execution]

**Status:** [Pass/Fail/Blocked]

**Notes:**
[Any additional information, links to bugs, screenshots]

---

### Grouping Structure:

**Positive Test Cases:** 
- Happy path scenarios
- Valid data entry
- Successful uploads/mappings

**Negative Test Cases:**
- Invalid data rejection
- Constraint violations
- Boundary condition errors

**Data Validation Test Cases:**
- Format validation
- Type validation
- Range validation

**Business Rule Test Cases:**
- Deductible ≤ Limit validation
- Coverage dependency rules
- Tax calculation rules
- Single-instance rules (e.g., only one OOC location)

**Integration Test Cases:**
- ZIP to ClaimsCentre data sync
- Coverage inheritance
- Multi-location scenarios
```

### Usage Example

**Input:**
```
User Story: Create Out of Country Location for Non-Canadian Insureds
Feature: Location Management - OOC Support
Acceptance Criteria: (10 criteria from Section 1A)
Coverage Types: Medical Payments, Bodily Injury, Financial Loss
System: ZIP Policy Management
```

**Expected Output:** (See Section 2A below)

---

## Section 2A: Test Case Suite - Out of Country Location

### Test Case Group: OOC Location Creation and Validation

#### TC-LOC-001: Create OOC Location with Valid Data
**Objective:** Verify that a new Out of Country location can be created with OOC country code and required fields populate correctly

**Preconditions:**
- User is logged in with Underwriter role
- Policy has been created for Accident & Health (LOB 057, Policy Type AH)
- No existing OOC location exists on the policy

**Test Data:**
- Country Code: OOC
- Address: "Out of Canada - A&H only"
- City: "Out of Canada - A&H only"
- Province: [Should be disabled/hidden]
- Postal Code: [Should be disabled/hidden]

**Steps:**
1. Navigate to "Maintain Policy" screen
2. Select "Locations" option
3. On "Work with Location" screen, press F9 to add location
4. On "Maintain Location" screen, select Country: OOC
5. Verify Address field auto-populates with "Out of Canada - A&H only"
6. Verify City field auto-populates with "Out of Canada - A&H only"
7. Verify Province field is hidden/disabled
8. Verify Postal Code field is hidden/disabled
9. Verify Cresta Zone field is blank and not required
10. Verify Windstorm Zone field is blank and not required
11. Verify Flood Zone field is blank and not required
12. Save the location

**Expected Result:**
- OOC location is created successfully
- All required fields are populated with correct values
- Disabled fields do not accept input
- Location is visible in location list
- No validation errors are displayed

---

#### TC-LOC-002: Verify Only One OOC Location Allowed Per Policy
**Objective:** Verify system prevents creation of multiple OOC locations on the same policy

**Preconditions:**
- Policy has an existing OOC location
- User has Underwriter role

**Test Data:**
- Attempt to create second OOC location with same data

**Steps:**
1. Navigate to existing policy with OOC location
2. Go to "Maintain Policy" > "Locations"
3. Press F9 to add new location
4. Select Country: OOC
5. Attempt to save

**Expected Result:**
- System displays error message: "Only one Out of Country location is allowed per policy"
- Location is NOT created
- Existing OOC location remains unchanged

---

#### TC-LOC-003: Create Province-Based Location Alongside OOC Location
**Objective:** Verify that province-based locations can coexist with a single OOC location

**Preconditions:**
- Policy has an existing OOC location
- User has Underwriter role

**Test Data:**
- New Location - Country: Canada
- Province: Ontario
- Address: "Toronto Branch"
- City: "Toronto"

**Steps:**
1. Navigate to policy with existing OOC location
2. Go to "Maintain Policy" > "Locations"
3. Press F9 to add new location
4. Select Country: Canada
5. Select Province: Ontario
6. Enter Address: "Toronto Branch"
7. Enter City: "Toronto"
8. Save location

**Expected Result:**
- New Ontario location is created successfully
- OOC location still exists
- Policy now has both OOC and Ontario locations
- No conflict or overlap errors

---

#### TC-LOC-004: Verify Tax Calculation is $0 for OOC Location
**Objective:** Verify that premium tax is calculated as $0 for OOC locations

**Preconditions:**
- Policy has OOC location
- Premium has been entered for OOC location
- Tax calculation rules configured

**Test Data:**
- Premium amount for OOC location: $10,000.00
- Expected Tax: $0.00

**Steps:**
1. Navigate to policy with OOC location
2. Enter Premium: $10,000.00
3. View Tax Calculation screen
4. Review calculated tax for OOC location

**Expected Result:**
- Tax displayed as: $0.00
- Total Premium after tax: $10,000.00
- Tax line shows: "Out of Country - No Tax Applied"

---

#### TC-LOC-005: Verify All Coverages Apply to OOC Location
**Objective:** Verify that all policy coverages automatically apply to OOC location

**Preconditions:**
- Policy has Medical Payments, Bodily Injury, and Financial Loss coverages
- OOC location has been created

**Test Data:**
- Existing Coverages: MP (Medical Payments), BI (Bodily Injury), FL (Financial Loss)

**Steps:**
1. Navigate to OOC location details
2. View Coverage section
3. Verify all active policy coverages are listed
4. Verify no manual coverage assignment was required

**Expected Result:**
- All three coverages (MP, BI, FL) are automatically assigned to OOC location
- Coverage limits and deductibles match policy-level definitions
- No warning or validation errors

---

#### TC-LOC-006: Verify ZIP to ClaimsCentre Data Sync for OOC Location
**Objective:** Verify OOC location data correctly syncs to ClaimsCentre

**Preconditions:**
- Policy with OOC location exists in ZIP
- ClaimsCentre integration is active
- All coverage claim questions configured

**Test Data:**
- OOC Location
- Coverage claim questions: BI, FL, MP, PD, PI, BD

**Steps:**
1. Create policy with OOC location and coverages in ZIP
2. Submit policy to ClaimsCentre
3. Retrieve policy data from ClaimsCentre
4. Verify OOC location is recognized
5. Verify claim questions map correctly to OOC

**Expected Result:**
- OOC location synced successfully to ClaimsCentre
- Claim questions (BI, FL, MP, PD, PI, BD) display correctly
- No mapping errors or missing data
- ClaimsCentre can process claims for OOC location

---

#### TC-LOC-007: Attempt Create OOC Location Without Required Authorization
**Objective:** Verify non-Underwriters cannot create OOC locations

**Preconditions:**
- User has limited role (e.g., Read-Only, Operator)
- Policy exists

**Test Data:**
- User Role: Operator
- Attempted Action: Create OOC location

**Steps:**
1. Log in with Operator role
2. Navigate to policy
3. Go to Locations section
4. Press F9 to add location
5. Select Country: OOC

**Expected Result:**
- Error message: "Insufficient permissions to create Out of Country locations"
- Location is NOT created
- System logs security event

---

#### TC-LOC-008: OOC Location Boundary Test - Verify Field Length Limits
**Objective:** Verify that OOC location address/city auto-populate strings respect system field length limits

**Preconditions:**
- OOC location creation screen open

**Test Data:**
- Auto-populate value: "Out of Canada - A&H only" (28 characters)
- System field limit: 50 characters (assumed)

**Steps:**
1. Select Country: OOC
2. Verify Address field contains: "Out of Canada - A&H only"
3. Verify City field contains: "Out of Canada - A&H only"
4. Check character count vs. field limit

**Expected Result:**
- Both fields successfully populate with 28-character string
- No truncation occurs
- No validation error for field length

---

#### TC-LOC-009: Negative Test - Attempt Manual Address Entry When OOC Selected
**Objective:** Verify that Address field is read-only/auto-populated when OOC is selected

**Preconditions:**
- OOC location creation in progress

**Test Data:**
- Attempt to enter: "123 Main Street"

**Steps:**
1. Select Country: OOC
2. Address field auto-populates with "Out of Canada - A&H only"
3. Attempt to clear address field
4. Attempt to type new address: "123 Main Street"

**Expected Result:**
- Address field is read-only
- Cannot clear or modify the auto-populated value
- Field displays as disabled/grayed out

---

#### TC-LOC-010: OOC Location Data Persistence Test
**Objective:** Verify that OOC location data is correctly persisted and retrievable

**Preconditions:**
- OOC location has been created and saved

**Test Data:**
- Created OOC Location ID: [Auto-generated]

**Steps:**
1. Create and save OOC location
2. Navigate away from policy
3. Return to same policy
4. View Locations section

**Expected Result:**
- OOC location is still visible
- All fields retain their values: Address, City, Zones
- Location appears in location list
- Can be edited/viewed without data loss

---

## Section 3: How to Use These Prompts

### For User Story Generation:
1. Copy the prompt template from Section 1
2. Fill in the [BRACKETED] placeholders with your feature information
3. Submit to your LLM (ChatGPT, Copilot, Claude, etc.)
4. Review and refine the output
5. Save the generated user story in `/OptimusCore/1_Base_Repo/Userstory/`

### For Test Case Generation:
1. Copy the prompt template from Section 2
2. Paste the acceptance criteria from the related user story
3. Fill in placeholders with feature and data details
4. Submit to your LLM
5. Review and refine the generated test cases
6. Organize by test case type (Positive, Negative, Validation, Business Rules, Integration)
7. Save in `/OptimusCore/3_Prompt_Config/` or `/OptimusCore/4_Designstudio/`

### Best Practices:
- **Be Specific:** Include exact field names, codes, and business rules from your ZIP system
- **Include Examples:** Reference real data from your policies (LOB codes, Policy Types, Coverage codes)
- **Think Integration:** Consider ClaimsCentre, tax systems, and other downstream impacts
- **Validate Constraints:** Include business rules like "Deductible ≤ Limit", "Max 1 OOC location"
- **Plan for Errors:** Include negative test cases and error handling scenarios
- **Document Dependencies:** Note what other features must be completed first
- **Cross-Reference:** Link user stories to their test cases
