# API Design

## Difference between SOAP and REST
| SOAP | REST |
| - | - |
| A fixed process | Few requirements |
| Lots of documents upfront | Docs discovered as you go |
| Detailed scenarios | Flexible, based on needs |
| Complex error handling | Flexible, based on patterns |

## REST API Constraint
1. Client-server architecture
2. Stateless architecture
   * Every request should be able to execute on its own
   * this gives stability, scalability and reliability to the entire system
3. Cacheable
   * know when to return results, instead of doing the work
   * Idempotent or Safe commands
   * | GET, PUT, DELETE | POST |
        | - | - |
        | the state of resources on the server is exactly the same after repeated commands | the state of resources on the server may change after repeated commands |
        | Cacheable | Often Not Cacheable |
4. Layered Systems
   * Clients may not be connected to the server *directly*
   * Leverage the layers providing flexibility to the system such as:
     * DNS lookups
     * Load balancers
     * Caching servers
     * Logging
     * Audit trails
     * Authentication
     * Authorization
5. Code on demand
   * When a client requests a resource, it also receives the code to act upon it, allows for flexibility, upgradability and extensibility
6. Uniform Interface
   * Identification of resources
   * Manipulation of resources through these representation
   * Self-descriptive messages
   * Hypermedia as the engine of application state (HATEOAS)
   * Our applications can discover links, where the client can request URLs from an API based on the name instead of URL itself

## Common Design Challenges
### Authentication and authorization
* | Authn | Authz |
    | - | - |
    | Authentication | Authorization |
    | Establish who you are | Establish your permissions |
    | Login with credentials | Restricted access |
* API Keys
  * | Benefits | Drawbacks |
    | - | - |
    | Easy to add to header or URL | URLs are not secret |
    | Framework and programming language agnostic | Difficult to update/rotate if compromised |
* OAuth
  * Authorization protocol
  * Upon authentication, a token maps to an authorization description
  * OAuth 2.0
    | Benefits | Drawbacks |
    | - | - |
    | Reliable and well established | Complicated |
    | Massive ecosystem | Initial implementation is time consuming |
    | Open-source and commercial options |  |

### API Versioning
* Accept header
  * more proper than URL
  * The accept header tells the API the data types and formats a client understands (content negotiation in accept header)
    * Establish the markup or notation (XML or JSON)
    * Establish the media type (structure of the markup)
    * Establish the version of the media type and resource
    * Client can ask for the version that best fits their needs
    * caters for Large scale APIs, optimize for clarity of purpose and ease of use
* URL
  * clear and explicit compared to accept header
  * nothing is lost with copy/paste
* Consistency is Key of applying versioning in an organization
  * simplify training
  * increase predictability for users
  * maintain clarity

### Content and Media Types
* What data is going in the payload and how should it be structured?
* JSON key:value pair
  * Difficult to extend and add details about data
* Media types
  * Shared data structures for JSON
  * Growing ecosystem
  * Supported by libraries
* **Collection + JSON**
  * contain a set of `links`, list of `items`, a `queries` collection, and a `template` object
* **Hypertext Application Language (HAL)**
  * separates the payload into two parts: data and _links
  * *drawbacks*:
    * can be verbose
    * having metadata in _links separate from data is odd; easy to lose context and not explore as appropriate
* **The Ion Hypermedia Type**
  * designed specifically to key data
  * metadate logically grouped and easier to process and apply
  * little use and few helper libraries and examples
  
### Hypermedia Approaches
* design the API in such a way that the APIs are **Non-Linear** - No Specified beginning, middle and end.
* each API request brings an independent set of available new API varieties which has no dependencies with previous API request

### HTTP Headers
* Content negotiation
  * Mechanisms which allow multiple versions of a document to exist at a single URL so the client-server can determine which version to use
  * Leverage libraries and tools to help implementing it
* Caching
  * A way of storing and retrieving data so that future requests can retrieve it faster, without duplicating an operation
  * ETags Request and Response
    1. The client makes a request
    2. The server responds and creates an ETag based on the resource state
    3. The client makes a HEAD request (same request as before)
    4. If the data is unchanged, the server returns the same ETags (complete)
    5. If the data has changed, the server returns a new ETag
    6. If the ETag is changed, the client makes the full request

### Documentation
* Goals:
  * snippet-friendly code
  * page history, specifically user facing (version control)
  * easy to update
  * searchable
* Example via Wiki:
  * MediaWiki
  * Confluence
  * Drawbacks:
    * It's either updated or not - there's no workflow or staging space in most systems
* Example via Static Site
  * Leverage generators (**Jekyll**)
    * Easy to configure
    * No version control built in: leverage GIT version control
    * Easy to maintain
    * Search engine friendly
    * Drawbacks:
      * It's still in raw text or markup which may be a challenge for your team
  * **Slate**
    * based on Jekyll, has all its benefits
    * Preconfigured with various code samples in mind
    * Language-specific samples are directly linkable
    * Consistent look and feel and navigation throughout the site

### SDK for APIs
* Build a great SDK experience
* SPOIL
  * S: *Succint*: concise but precise
  * P: *Purposeful*: apply the same care as you would to the API
  * O: *Open Source*: encourage wrappers, extensions, user contributions
  * I: *Idiomatic*: use the patterns and conventions of the language
  * L: *Logical*: be consistent and repeat common patterns