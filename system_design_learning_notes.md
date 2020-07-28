# System Design

## Snake
1. Scenario
2. Nessecary:
3. Application:
4. Kilobat
5. Evolve


## Principles

### [Pattern: Backends For Frontend](https://samnewman.io/patterns/architectural/bff/#)
   - When you don't have BFFs, then often the 'common' logic ends up being baked into the different clients themselves
   - [Other](http://www.ayqy.net/blog/backend-for-frontend-bff/)

### [Strangler fig problem](https://martinfowler.com/bliki/StranglerFigApplication.html)
  - How to maintain the old code base and at the mean time rewrite/refactor the code
  - An alternative route is to gradually create a new system around the edges of the old, letting it grow slowly over several years until the old system is strangled
  - When designing a new application you should design it in such a way as to make it easier for it to be strangled in the future. Let's face it, all we are doing is writing tomorrow's legacy software today