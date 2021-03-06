

# Module shackle_server #
* [Data Types](#types)
* [Function Index](#index)
* [Function Details](#functions)

<a name="types"></a>

## Data Types ##




### <a name="type-backlog_size">backlog_size()</a> ###


<pre><code>
backlog_size() = pos_integer() | infinity
</code></pre>




### <a name="type-client">client()</a> ###


<pre><code>
client() = module()
</code></pre>




### <a name="type-client_option">client_option()</a> ###


<pre><code>
client_option() = {ip, <a href="inet.md#type-ip_address">inet:ip_address()</a> | <a href="inet.md#type-hostname">inet:hostname()</a>} | {port, <a href="inet.md#type-port_number">inet:port_number()</a>} | {protocol, <a href="#type-protocol">protocol()</a>} | {reconnect, boolean()} | {reconnect_time_max, <a href="#type-time">time()</a>} | {reconnect_time_min, <a href="#type-time">time()</a>} | {socket_options, [<a href="gen_tcp.md#type-connect_option">gen_tcp:connect_option()</a> | <a href="gen_udp.md#type-option">gen_udp:option()</a>]}
</code></pre>




### <a name="type-client_options">client_options()</a> ###


<pre><code>
client_options() = [<a href="#type-client_option">client_option()</a>]
</code></pre>




### <a name="type-client_state">client_state()</a> ###


<pre><code>
client_state() = term()
</code></pre>




### <a name="type-pool_name">pool_name()</a> ###


<pre><code>
pool_name() = atom()
</code></pre>




### <a name="type-pool_option">pool_option()</a> ###


<pre><code>
pool_option() = {backlog_size, <a href="#type-backlog_size">backlog_size()</a>} | {pool_size, <a href="#type-pool_size">pool_size()</a>} | {pool_strategy, <a href="#type-pool_strategy">pool_strategy()</a>}
</code></pre>




### <a name="type-pool_options">pool_options()</a> ###


<pre><code>
pool_options() = [<a href="#type-pool_option">pool_option()</a>]
</code></pre>




### <a name="type-pool_size">pool_size()</a> ###


<pre><code>
pool_size() = pos_integer()
</code></pre>




### <a name="type-pool_strategy">pool_strategy()</a> ###


<pre><code>
pool_strategy() = random | round_robin
</code></pre>




### <a name="type-protocol">protocol()</a> ###


<pre><code>
protocol() = shackle_tcp | shackle_udp
</code></pre>




### <a name="type-reconnect_state">reconnect_state()</a> ###


<pre><code>
reconnect_state() = #reconnect_state{current = undefined | <a href="#type-time">time()</a>, max = <a href="#type-time">time()</a> | infinity, min = none | <a href="#type-time">time()</a>}
</code></pre>




### <a name="type-server_name">server_name()</a> ###


<pre><code>
server_name() = atom()
</code></pre>




### <a name="type-state">state()</a> ###


<pre><code>
state() = #state{client = <a href="#type-client">client()</a>, header = iodata(), ip = <a href="inet.md#type-ip_address">inet:ip_address()</a> | <a href="inet.md#type-hostname">inet:hostname()</a>, name = <a href="#type-server_name">server_name()</a>, parent = pid(), pool_name = <a href="#type-pool_name">pool_name()</a>, port = <a href="inet.md#type-port_number">inet:port_number()</a>, protocol = <a href="#type-protocol">protocol()</a>, reconnect_state = undefined | <a href="#type-reconnect_state">reconnect_state()</a>, socket = undefined | <a href="inet.md#type-socket">inet:socket()</a>, socket_options = [<a href="gen_tcp.md#type-connect_option">gen_tcp:connect_option()</a> | <a href="gen_udp.md#type-option">gen_udp:option()</a>], timer_ref = undefined | reference()}
</code></pre>




### <a name="type-time">time()</a> ###


<pre><code>
time() = pos_integer()
</code></pre>

<a name="index"></a>

## Function Index ##


<table width="100%" border="1" cellspacing="0" cellpadding="2" summary="function index"><tr><td valign="top"><a href="#init-5">init/5</a></td><td></td></tr><tr><td valign="top"><a href="#start_link-4">start_link/4</a></td><td></td></tr><tr><td valign="top"><a href="#system_code_change-4">system_code_change/4</a></td><td></td></tr><tr><td valign="top"><a href="#system_continue-3">system_continue/3</a></td><td></td></tr><tr><td valign="top"><a href="#system_get_state-1">system_get_state/1</a></td><td></td></tr><tr><td valign="top"><a href="#system_terminate-4">system_terminate/4</a></td><td></td></tr></table>


<a name="functions"></a>

## Function Details ##

<a name="init-5"></a>

### init/5 ###

<pre><code>
init(Name::<a href="#type-server_name">server_name()</a>, PoolName::<a href="#type-pool_name">pool_name()</a>, Client::<a href="#type-client">client()</a>, ClientOptions::<a href="#type-client_options">client_options()</a>, Parent::pid()) -&gt; no_return()
</code></pre>
<br />

<a name="start_link-4"></a>

### start_link/4 ###

<pre><code>
start_link(Name::<a href="#type-server_name">server_name()</a>, PoolName::<a href="#type-pool_name">pool_name()</a>, Client::<a href="#type-client">client()</a>, ClientOptions::<a href="#type-client_options">client_options()</a>) -&gt; {ok, pid()}
</code></pre>
<br />

<a name="system_code_change-4"></a>

### system_code_change/4 ###

<pre><code>
system_code_change(State::<a href="#type-state">state()</a>, Module::module(), OldVsn::undefined | term(), Extra::term()) -&gt; {ok, <a href="#type-state">state()</a>}
</code></pre>
<br />

<a name="system_continue-3"></a>

### system_continue/3 ###

<pre><code>
system_continue(Parent::pid(), Debug::[], X3::{<a href="#type-state">state()</a>, <a href="#type-client_state">client_state()</a>}) -&gt; ok
</code></pre>
<br />

<a name="system_get_state-1"></a>

### system_get_state/1 ###

<pre><code>
system_get_state(State::<a href="#type-state">state()</a>) -&gt; {ok, <a href="#type-state">state()</a>}
</code></pre>
<br />

<a name="system_terminate-4"></a>

### system_terminate/4 ###

<pre><code>
system_terminate(Reason::term(), Parent::pid(), Debug::[], State::<a href="#type-state">state()</a>) -&gt; none()
</code></pre>
<br />

