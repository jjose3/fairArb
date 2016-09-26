Fair Priority 
When one resource is shared among many agents, those
agents must bid on the resource before using it. An arbiter indicates which agent has
won the resource. A simple implementation might assign static priority (e.g. MSB
bidder will always beat LSB bidder), however when congestion is high this can result
in the low priority bidders being effectively blocked. In this component we will explore
how we might guarantee that all bidders will eventually be able to make forward
progress.

// fairArb.vp
//; my $bW = parameter( name=>"bitWidth", val=>16, doc=>"Width of input");
module `mname` (
input logic [`$bW-1`:0] bids,
output logic [`$bW-1`:0] wins,
input logic clk,
input logic rst
);
// Empty module
endmodule: `mname`

The fairArb unit will receive a set of bids every cycle (a bit string where one indicate
bid and a zero indicates no-bid for each of 16 agents) and must return the winning bid
in the next cycle as a one-hot bit string. Formally, this means that the wins bit-string
must be one-hot or zero. If the winning string is one hot, the hot bit must have been
a bid in the prior cycle. There is not guarantee that a non-winning bid will bid again
on the next cycle or that a winning bid will not bid again. There is also no guarantee
that probability of a bid is uniform, independent, or identically distributed among each
of the agents. It is not expected that your design meet timing. Your design will be
functionally correct if it produces “legal” winners. Your design will also be evaluated
on its “fairness”. A fair design will have a small difference between the probability
of winning for an agent most likely to win and the agent least likely to win given a
specific bid (ideally the probabilities are identical). A part of your test strategy should
be to find problematic patterns for your design to test its “fairness”.

