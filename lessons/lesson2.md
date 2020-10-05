## Lesson 2: Set up alarms feed with trigger and rule

Let's first try the `/whisk.system/alarms/interval` feed of the OpenWhisk Alarm Package to [fire trigger events on an interval base schedule](https://github.com/apache/openwhisk-package-alarms#firing-a-trigger-event-periodically-on-an-interval-based-schedule). To see the effect instantly, we will make it run every minute. You will need a [trigger](https://github.com/apache/openwhisk/blob/master/docs/triggers_rules.md#creating-triggers) set up with the `/whisk.system/alarms/interval` feed, and a [rule](https://github.com/apache/openwhisk/blob/master/docs/triggers_rules.md#using-rules) to wire this trigger to the `generic` action created earlier.

The only required param for `interval` feed is `minutes`, which is an integer representing the length of the interval (in minutes) between trigger fires. Optional params are `trigger_payload`, `startDate` and `stopDate`.

```yaml
packages:
  __APP_PACKAGE__:
    license: Apache-2.0
    actions:
      generic:
        function: actions/generic/index.js
        runtime: 'nodejs:12'
        inputs:
          LOG_LEVEL: debug
        annotations:
          final: true
    triggers:
      everyMin:
        feed: /whisk.system/alarms/interval
        inputs: 
          minutes: 1
    rules:
      everyMinRule:
        trigger: everyMin
        action: generic
```

To test the trigger schedule, simply deploy the app again with `aio app deploy`, and observe that the action is invoked after 1 - 2 minutes with `aio rt activation list`.

![activation-list](assets/activation-list.png)

[Next](lesson3.md)