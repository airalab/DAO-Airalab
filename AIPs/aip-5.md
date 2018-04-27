<pre>
  Title: Add Objective field in the Bid message
  Author: Konstantin Danilov <mail@xomak.net>
  Status:
</pre>

# Add Objective field in the Bid message

The current structure of a Bid message and Lighthouse's logic could limit the number of possible applications for the robonomics protocol. Probably, such markets can be defined as markets, where an Ask is posted to the market prior to the Bid. For instance, this case could be explained, using the taxi market, where there are passengers and drivers. Let's assume, that this situation takes place in a megacity. As we know, the Ask has model and objective fields. The former represents a service model in general (in our case service is transportation within the city from point A to point B). The latter one assigns to A and B specific locations, within the city. Passenger (or agent, special software, etc.) could set any price for his ask, however "market will decide", whether this price is reasonable or not. In the same time obviously this price depends at least on the distance (and on any other external factors, like weather, district rating, etc).
Also, drivers have their own interests (for instance, they are ready to make a discount for the passenger, whose destination point is in driver's district, when he goes home). 

In my opinion, the problem with the current architecture is that it is not possible to provide services, with price depending on their objective, i.e. driver can not say to the market "I can provide taxi service from A to B for 5 XRT", he can just say "I can provide taxi service for 5 XRT". Therefore, mechanisms, which currently take place in the real world will not work. 

Three possible solutions are considered.

## Do not change anything
We can think, that if service price depends on the objective, than there are several services. I think, in some cases it could be true, but, for instance, not for the described above taxi service. In case of taxi service it is required to artificially create many models instead of one, however in the spirit they are the same. 

Let's imagine, that instead of one "transportation within the city" service, now we have "transportation from district A to B", "transportation from district B to A", "transportation from district C to B", "transportation from district B to A", etc. The first problem is that we have to somehow distinguish between "transportation" services and other services, which can be handled by the same lighthouse. The next problem is redundancy. For instance, service model can contain a model for further validation and other information, which will be duplicated in each "service". The third problem is that driver still can have some conditions, preventing him from providing the service. Probably, they could be explicitly written in the model, making it too complex.


## Simple Objective field
Another solution is to add the optional objective field in the Bid message and modify Liability creation condition: prevent liability creation, if the Bid contains objective and this objective does not match Ask's objective.
This solution does not break existing logics, because it is possible to set null value for Bid's objective and existing logic will work. However, if a service provider wants to broadcast his readiness to provide the service with specific objective for specific price, he can easily do it. This improvement could make system more flexible and requires minimal changes. 

One possible drawback is introducing an ability to create objectives, directed to specific predefined service provider. However, it is possible in existing architecture by creating new specific service models.

## Complex formulas
More complex solution is to strictly define, that objective is a dictionary with some model parameteres names and values. Also we can define formula, which is a simple boolean formula, which can include simple comparison functions, accepting model parameters. Now it is possible to define an Ask and a Bid, using a formula. Now matching process should be based on formulas intersection, finding parameter values, making both formulas true. The mechanism seems to be flexible and also can be introduced as additional to the existing one, however implementation is not so simple, especially, check procedure in smart contract implementation. Also, parameters intersection range can be relatively large, meaning, that many different parameters sets would match formulas. The lighthouse does not know their meaning and can not select the final set with respect to some optimum. Furthermore, this complex logic could be implemented on market's members side: they can exhange asks and bids, changing the objective, as long as they do not find optimal objective for both of them. 

## Conclusion
To conclude, I think, that current robonomics architecture is not easy and straightforward to use with some existing markets, for instance, where a Bid is sent to the market after an Ask. I met this problem during my work on Duckietown Taxi prototype and Distributed Sky project. Solution with complex formulas seems to be overcomplicated, at least at the current moment. I believe, that the optimal solution for now is to add Objective field in Bid message and change lighthouse's behavior, as it was described. This solution is easy to implement, does not break existing mechanism and makes the system more flexible.
