### Question

Imagine a web server for a simplified search engine. This system has 100 machines to respond to search queries, which may then call out using `processSearch(String query)` to another cluster of machines to actually get the result. The machine which responds to a given query is chosen at random, so you cannot guarantee that the same machine will always respond to the same request. The method `processSearch` is very expensive. Design a caching mechanism for the most recent queries. Be sure to explain how you would update the cache when data changes.
