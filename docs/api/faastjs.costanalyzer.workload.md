---
id: faastjs.costanalyzer.workload
title: CostAnalyzer.Workload interface
hide_title: true
---
[faastjs](./faastjs.md) &gt; [CostAnalyzer](./faastjs.costanalyzer.md) &gt; [Workload](./faastjs.costanalyzer.workload.md)

## CostAnalyzer.Workload interface

A user-defined cost analyzer workload for [CostAnalyzer.analyze()](./faastjs.costanalyzer.analyze.md)<!-- -->.

Example:

<b>Signature:</b>

```typescript
interface Workload<T extends object, A extends string> 
```

## Properties

|  Property | Type | Description |
|  --- | --- | --- |
|  [concurrency](./faastjs.costanalyzer.workload.concurrency.md) | <code>number</code> | The amount of concurrency to allow. Concurrency can arise from multiple repetitions of the same configuration, or concurrenct executions of different configurations. This concurrency limit throttles the total number of concurrent workload executions across both of these sources of concurrency. Default: 64. |
|  [format](./faastjs.costanalyzer.workload.format.md) | <code>(attr: A, value: number) =&gt; string</code> | Format an attribute value for console output. This is displayed by the cost analyzer when all of the repetitions for a configuration have completed. The default returns <code>${attribute}:${value.toFixed(1)}</code>. |
|  [formatCSV](./faastjs.costanalyzer.workload.formatcsv.md) | <code>(attr: A, value: number) =&gt; string</code> | Format an attribute value for CSV. The default returns <code>value.toFixed(1)</code>. |
|  [repetitions](./faastjs.costanalyzer.workload.repetitions.md) | <code>number</code> | The number of repetitions to run the workload for each cost analyzer configuration. Higher repetitions help reduce the jitter in the results. Repetitions execute in the same FaastModule instance. Default: 10. |
|  [silent](./faastjs.costanalyzer.workload.silent.md) | <code>boolean</code> | If true, do not output live results to the console. Can be useful for running the cost analyzer as part of automated tests. Default: false. |
|  [summarize](./faastjs.costanalyzer.workload.summarize.md) | <code>(summaries: WorkloadAttribute&lt;A&gt;[]) =&gt; WorkloadAttribute&lt;A&gt;</code> | Combine [CostAnalyzer.WorkloadAttribute](./faastjs.costanalyzer.workloadattribute.md) instances returned from multiple workload executions (caused by value of [CostAnalyzer.Workload.repetitions](./faastjs.costanalyzer.workload.repetitions.md)<!-- -->). The default is a function that takes the average of each attribute. |
|  [work](./faastjs.costanalyzer.workload.work.md) | <code>(faastModule: FaastModule&lt;T&gt;) =&gt; Promise&lt;WorkloadAttribute&lt;A&gt; &#124; void&gt;</code> | A function that executes cloud functions on <code>faastModule.functions.*</code>. The work function should return <code>void</code> if there are no custom workload attributes. Otherwise, it should return a [CostAnalyzer.WorkloadAttribute](./faastjs.costanalyzer.workloadattribute.md) object which maps user-defined attribute names to numerical values for the workload. For example, this might measure bandwidth or some other metric not tracked by faast.js, but are relevant for evaluating the cost-performance tradeoff of the configurations analyzed by the cost analyzer. |