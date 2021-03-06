---
-api-id: P:Windows.ApplicationModel.Background.TimeTrigger.FreshnessTime
-api-type: winrt property
---

<!-- Property syntax
public uint FreshnessTime { get; }
-->

# Windows.ApplicationModel.Background.TimeTrigger.FreshnessTime

## -description
Gets the interval of a time event trigger.

## -property-value
Specifies the number of minutes to wait before scheduling the background task. The system schedules the task within 15 minutes after [FreshnessTime](timetrigger_freshnesstime.md) elapses.

## -remarks
The system uses a 15-minute tick frequency for timer requests. A time-triggered background task is scheduled on the next tick after [FreshnessTime](timetrigger_freshnesstime.md) elapses. If the [OneShot](timetrigger_oneshot.md) property is false, [FreshnessTime](timetrigger_freshnesstime.md) specifies the interval for a recurring task.



> [!NOTE]
> If *FreshnessTime* is set to less than 15 minutes, an exception is thrown when attempting to register the background task.

## -examples

## -see-also
