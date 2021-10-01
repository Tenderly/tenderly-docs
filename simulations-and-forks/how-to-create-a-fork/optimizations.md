# Optimizations



1. The longer the simulation chain for a fork gets, the more important it is to have a proper state merging strategy and layout to reduce the amount of overhead we have preparing the simulation payload. 
   * Initially, it could be sufficient to simply record the state emitted by a simulation in the same table as a JSONB field and query and process the entire fork state in bulk. 
   * However, with the longer chains of simulations we might run into difficulties performing that information pull and processing in a short enough timeframe. 
   * An alternative approach can be splitting the resulting state and the simulation payload into two separate tables, and setup the state table to better handle the case of pulling the appropriate state for a simulation directly with a single query. 
2. Each simulation in a particular fork can have a **cold** and a **hot** start in regard to state needed to reliably run the simulation. 
   * When cold starting, we don't know which elements of the forked state will be needed by the simulated transaction, so we need to pass all the state that we accumulated since starting the fork. 
   * Once the cold start has been completed, we can record which state items actually got used in the simulation, and we can record that information for later use. 
   * This record of used state items allows us to later re-simulate the same transaction by hot starting it. 
   * A hot start is an optimized call to the simulator, which sends only the state items specified by the cold start as being "in-use".

