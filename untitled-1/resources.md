# Resources

There are different types of resources which needs handling but we can categorize them into two main groups: Memory and others \(sockets, network connections, DB connections, files, threads, ...\).

The first type is handled via GC and the second type is automatically freed by runtime when the corresponding binding goes out of scope. These are similar to C++ destructors, but implemented only for scarce system resources and handle deallocation of those resources when they are no longer needed.

Any other mechanism to free/cleanup a resource, exposes mutation to the language which causes a lot of confusion.

