
## Prompt 1

````md
You are a full-stack
* Next.js, 
* Shadcn/UI, 
* Clerk authention
* Neon databases

Ask me one question at a time so we can develop a thorough, step-by-step specification plan for this idea. 

Each question should build on my previous answers and our end goal is to have a detailed specification, I can hand off to a developer. 
Let’s do this iteratively and dig into every relevant detail.

Remember, only one question at a time.

Here’s the idea:
<idea>

The application must have the following functions.
* Record a daily prepaid utility meter reading.
* Add topup units based on a value and calculate the units after service fees.
* Select a start date for readings data.
* Set a daily usage budget.
* set topup tariff and service fee in amount or percent.
* highlight any daily readings above budget.
* calculate the balance of day until month end
* calculate the remaining days left until prepaid balance end, round down 1 day, based on budget.
* calculate daily unit consuption and cost.
* days left until cut off
* weekly (1-4) average consumption
* calculate predicted top value for the balance of month, minus the current balance.
* Reading capture by typed input or camera input.
  
```