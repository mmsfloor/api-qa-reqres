# API Testing Summary

This document summarizes observations that were made during the API testing process that are not considered functional defects but may represent potential quality, design, or robustness risks.


## Test Coverage
All API scenarios were correctly executed based on the available API documentation.
There were no contract violations.

Additionally, I conducted exploratory and negative testing to evaluate how the API handles edge cases and undocumented scenarios.


## Test Execution Summary

| Status        | Count | Description                                         |
|---------------|-------|-----------------------------------------------------|
| Passed        | 24    | Behavior matches documented or expected contract    |
| Inconclusive  | 4     | Behavior observed, requirements not clearly defined |
| Failed        | 0     | —                                                   |
| Blocked       | 0     | —                                                   |

Inconclusive test cases indicate areas where system behavior cannot be evaluated against explicit acceptance criteria due to missing or unclear documentation.


## Observations

### OBS-01: Missing Input Length Validation

**Related Test Cases:** TC-014  
**Endpoints:** POST /users  
**Category:** Input Validation  
**Risk Level:** Medium  

**Description:**  
The API accepts excessively long input values (name length exceeding 10000 characters) and the request is processed successfully without any validation errors.

**Impact:**  
Without limits on input length, this may lead to several issues:
- Increased storage use and database bloat
- Slower performance due to larger payloads
- Possible abuse scenarios (like DoS attacks using oversized requests)

**Notes:**  
Input length limits are not specified in the documentation, so this behavior is technically contract-compliant. However, defining and enforcing reasonable limits would improve API robustness.


### OBS-02: Silent Fallback on Invalid Query Parameters

**Related Test Cases:** TC-020  
**Endpoints:** GET /users  
**Category:** API Contract / Error Handling  
**Risk Level:** Low  

**Description:**  
When an invalid query parameter value is provided (`page=abc`), the API returns `200 OK` and defaults to the first page silently.

**Impact:**  
In this case, the silent fallback may mask client-side validation issues and make API more unpredictable. Developers might not realize their input was ignored, which complicates debugging.

**Notes:**  
The expected behavior for invalid parameter types is not documented. 
Industry practice suggests returning `400 Bad Request` with a clear error message, though silent fallback is also a valid design choice if properly documented.


### OBS-03: Update Operation on Non-Existent Resources

**Related Test Cases:** TC-025  
**Endpoints:** PUT /users/{id}  
**Category:** API Design / Data Consistency  
**Risk Level:** High  

**Description:**  
An attempt to update a non-existent user ID returns `200 OK` with updated user information, despite the resource not previously existed.

**Impact:**  
It could be a sign of an undocumented *upsert* functionality, but it can be surprising if clients expect standard RESTful semantics (where PUT on a missing resource typically returns `404 Not Found`).

**Notes:**  
It is unclear from the API documentation whether update operations should create a new resource when the target ID does not exist.


### OBS-04: Delete Operation on Non-Existent Resources

**Related Test Cases:** TC-028  
**Endpoints:** DELETE /users/{id}  
**Category:** API Design / Idempotency  
**Risk Level:** Low  

**Description:**  
Deleting a non-existent user returns `204 No Content`.

**Impact:**  
While acceptable for idempotent delete operations, the absence of documented behavior may cause uncertainty for API consumers.

**Notes:**  
Both `204 No Content` and `404 Not Found` are acceptable industry practices, but the expected behavior should be explicitly documented.


## Conclusion
The API fulfills all documented functional requirements and demonstrates stable behavior for core use cases.

The observations listed above represent quality and design considerations rather than functional defects. 
These aren't bugs, but they do represent opportunities to improve clarity and predictability.
