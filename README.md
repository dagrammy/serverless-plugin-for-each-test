# serverless-plugin-for-each-test

How to install & start:
```
yarn install
yarn package
```

configuration:
```
custom:
  rate:
    - RATE_A
    - RATE_B
  cron:
    - CRON_Z
    - CRON_Y
    - CRON_X
```

iterators:
```
Resources:
  $forEach:
    iterator: "${self:custom.rate}"
```

```
Resources:
  $forEach:
    iterator: "${self:custom.cron}"
```

created `cloudformation-template-update-stack.json`
```
    "RateScheduleCRON_Z": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "rate(5 minutes)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_Z\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "CronScheduleCRON_Z": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "cron(0 8 * * ? *)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_Z\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "RateScheduleCRON_Y": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "rate(5 minutes)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_Y\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "CronScheduleCRON_Y": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "cron(0 8 * * ? *)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_Y\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "RateScheduleCRON_X": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "rate(5 minutes)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_X\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "CronScheduleCRON_X": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "cron(0 8 * * ? *)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_X\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    }
  }
```

expected result:
```
    "RateScheduleRATE_A": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "rate(5 minutes)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"RATE_A\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "RateScheduleRATE_B": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "rate(5 minutes)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"RATE_B\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "CronScheduleCRON_Z": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "cron(0 8 * * ? *)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_Z\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "CronScheduleCRON_Y": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "cron(0 8 * * ? *)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_Y\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    },
    "CronScheduleCRON_X": {
      "Type": "AWS::Events::Rule",
      "Properties": {
        "ScheduleExpression": "cron(0 8 * * ? *)",
        "Targets": [
          {
            "Input": "{\"scheduler\":\"CRON_X\"}",
            "Arn": "arn:aws:lambda:eu-central-1:123456789:function:callIt",
            "Id": "callItId"
          }
        ]
      }
    }
}
```