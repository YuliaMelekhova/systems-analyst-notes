# STRIDE Threat Modeling

Threat models cross-linked to the requirements and API specifications they change, rather than filed where nobody checks them mid-build. The content is the same either way. What differs is whether the analyst writing acceptance criteria can see the threat from where they are working.

A model belongs here when it covers one concrete flow with its trust boundaries drawn, and when every finding in it names the artifact that has to change. A threat producing no change to any requirement, contract or test case was an observation, and observations do not ship.

Models are re-run when a boundary moves, which means a new vendor, a split service or a newly exposed endpoint. A calendar review on an unchanged flow finds nothing.
