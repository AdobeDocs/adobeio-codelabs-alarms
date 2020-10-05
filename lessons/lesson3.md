## Lesson 3: Types of alarm feed

Apart from the `/whisk.system/alarms/interval` feed in lesson 2, the alarms provider in Adobe I/O Runtime supports other types of feed.

### Firing a trigger once

The `/whisk.system/alarms/once` feed allows you to [fire event once at a specific time](https://github.com/apache/openwhisk-package-alarms#firing-a-trigger-event-once). The only required param is `date` to indicate when the trigger is fired. Optional params are `trigger_payload` and `deleteAfterFire`.

```yaml
triggers:
  runMeOnce:
    feed: /whisk.system/alarms/once
    inputs: 
      date: YYYY-MM-DDTHH:mm:ss.sssZ
      deleteAfterFire: true
```

Please note that `YYYY-MM-DDTHH:mm:ss.sssZ` is just a format for this field. You are free to update it with the exact date and time you want.

### Firing a trigger on a time-based schedule using cron

The `/whisk.system/alarms/alarm` feed allows you to [fire event on a time-based schedule using cron](https://github.com/apache/openwhisk-package-alarms#firing-a-trigger-on-a-time-based-schedule-using-cron). This is more generic than the `interval` and `once` feeds, because you can write crontab to configure the alarm service to trigger at the exact time and interval as you wish. The only required param is `cron`, which is a string based on the [UNIX crontab syntax](http://crontab.org) that indicates when to fire the trigger in UTC. Optional params are `trigger_payload`, `timezone`, `startDate` and `stopDate`. 

The following example shows a cron schedule at 2am on Sundays.

```yaml
triggers:
  sunday2am:
    feed: /whisk.system/alarms/once
    inputs: 
      cron: 0 2 7 * *
      timezone: CET
      startDate: 1601918992704
      stopDate: 1651918992704
```

Next lesson: [Well done](welldone.md)