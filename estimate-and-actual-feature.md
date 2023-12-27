# Differentiate Estimate events from Actual events Feature

**Summary**

Allow users to specify and track if data for an event is estimated or based on actual figures. Segment events based on this for reporting.


**Goals**

- Store estimated vs actual indicator with events
- Include estimate/actual label prominently on event dashboard
- Include edit feature to allow users switch between actual and estimate status
- Display and toggle between estimate and actual event status on company dashboard 
- Collect with analytics events 
- Enable filtering between estimated vs actual
- Segment analytics to differentiate between events with estimated vs validated data to exclude unreliable numbers from insights.

**User Stories**

- As an event organizer, I want to mark events as estimated counts when I am early in the planning phase and don't have final numbers.
- As a TRACE admin, I want to know which reports are estimated or actual to provide greater insight when producing reports.


## Implementation

**Backend**

- Add `eventEstimateOrActual` field to Event model
   - Values: `"Estimate", "Actual"`
   - Required 
- Validate in controller
  - If missing, 400 error
- On create/update, store submitted value
- Return in GET event endpoints 
- Script to ensure backward compatibility for existing events
- Logging to provide details on database update
- Update backend API endpoints for event creation and editing to handle new field and persist information in database
- End-to-end tests to validate entire feature workflow.

**Frontend**

- Add radio selector to event forms
  - Specify Required  
- Fetch options from language files
- Connect to Redux filter state
- Submit as part of event object

**Analytics**

- Track new property in Mixpanel 


**Considerations**

- Ensure backward compatibility with existing events that do not have the `eventEstimateOrActual` field.
- Database backup for rollback procedure
- Plan for data migration if necessary for existing events without the new field.



## Exploratory

- Integrate with existing non-analogous Open/Closed event status?
- Default existing events to Estimate? 