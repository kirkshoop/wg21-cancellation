# wg21-cancellation
repo for D1677 'Cancellation is not an Error'

This is using the wg21 paper framework by @mpark ([Requirements](https://github.com/mpark/wg21/blob/master/README.md#requirements) & [Formatting](https://github.com/mpark/wg21/blob/master/README.md#formatting))

latest ([pdf](generated/cancellation.pdf), [html](generated/cancellation.html), [slides](slides/cancellation.html))

Audience
  - SG1 Concurrency and Parallelism
  - SG13 IO
  - LEWG Library Evolution
  - EWG Evolution

# Changelog

__R1__

 - [x] Use bibliography for Cologne paper references
 - [x] add stack-frame analogy for callbacks
 - [x] add `fiber_context` unwind mechanisms
 - [x] add section on non-cpp-exception
 - [x] add code to show `throw(...)` usages that break unwind by exception
 - [x] fix code examples (apply Lewis' feedback)
 - [x] add `f(g(h()))`, `generator` & `retry` examples 
 - [x] switch the term neither-a-result-nor-an-error to serendipitous-success

# Introduction

One of the basis operations for any async function is cancellation. In this paper we explore the uses of cancellation to determine how to represent the result of a cancelled async function (the mechanism to signal a request for cancellation is covered by `stop_source` in C++20). In this paper a cancelled result is described as an instance of serendipitous-success ([Credits] go to Lisa Lippincott for coining this term).

The ideas in this paper have proved to be exceedingly difficult to communicate. Each time this conversation is begun with a new person the same process of exploring the options to represent a cancelled result from a function is repeated. 

It is usually easy to discard using an `optional<T>` return value. This ease is due to the noise it introduces, so we can skip the much harder task of explaining that the return value is a poor representation of a cancelled result. 

We cannot avoid the hard task of explaining why something like a `cancelled_error` exception or `error_code` is a poor representation of a cancelled result, because it does not appear at first glance to introduce a lot of noise. This paper is focused on explaining why errors are a bad way to represent a cancelled result.
