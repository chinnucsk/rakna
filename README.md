Räkna - You Count On It!
=================

#### 1 Overview
#### 2 Quick Start 
    2.1 Building Räkna
    2.2 Starting Räkna
    2.3 Räkna's REST API 


#### 1 Overview


Räkna, pronounced: "wreck nah" according to Google's English->Swedish translation, is intended to be a time-series based, (soon-to-be) distributed, incremental/decremental 
counting mechanism with support for integers and floats.

Why?

I wanted a way to reliably store counters over a period of time (dates for now). I need this for everything from counting allele frequencies coming off of genotyping instrumentation to fantasy-sports points gathering.
You could also throw in web-metrics for gits and shiggles, but I think that's one of the more obvious use cases.

What's under the hood? (aside from the rushed API)

 Basho's eleveldb storage for persistent data for starters.
 Ulf Wiger's sext library for aiding leveldb with sequential writes (took this trick from the leveldb driver in Riak).
 Basho's webmachine for a rock-solid REST API.
 Mochiweb via Webmachine for JSON encoding


#### 2 Quick Start


	2.1 Building Räkna

		Via rebar:
		1. ./rebar get-deps
		2. ./rebar compile
		3. ./rebar generate

	2.2 Starting Räkna

		./rel/rakna-node/bin/rakna-node [start|console] (pick either one)

	2.3 Räkna REST API

		Assuming you used the defaults, you can access counters this way:
		GET http://127.0.0.1:8088/counters/[counter name]
			Be sure to use a Content-Type of: application/json
			
	2.4 Räkna Erlang API

		Assuming you are running in a console, or have it loaded via an application:

		Incrementing

		rakna_node:increment(Key)
		rakna_node:increment(Date :: tuple(), Key)
		rakna_node:increment(Key, Amount)
		
		Decrementing

		rakna_node:decrement(Key)
		rakna_node:decrement(Date :: tuple(), Key)
		rakna_node:decrement(Key, Amount)
		
		Reading

		rakna_node:get_counter(Key)
		rakna_node:get_counter(Date :: tuple(), Key)
		
		All increment/decrement functions are synchronous. For asynchronous versions use the a_increment/a_decrement version.
