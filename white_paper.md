Sponsor Contract  
-----------------------------
-----------------------------

Actors
------
Three types of actors interact with the Sponsor Contract (SC). The sponsor Alice, to fix ideas, the beneficiary Bob, and Sarah's service. 

**Alice** can:

#### Actions
1. Grant an allowance to Bob to be used with Sarah's service. This allowance can only be used with Sarah's and will be transfered to SC. 
2. Withdraw at any time her unspent funds from SC. 

#### Views
3. View her funded and unspent allowances.

**Bob** can:

#### Actions
1. Sign contracts with Sarah's service spending Alice's allowance, which will be cashed out by SC. 

#### Views
2. View all his allowances.

**Sarah** can:

#### Actions
1. Receive transfers from SC when Bob is contracting her service (see Bob 1.).
2. Increase Bob's allowance without transfering tokens to SC. In other words, Sarah can offer Bob a discount. Sarah can set discount limits in form of percentages and total volume of the deal to prevent disadvantage from small deals.
3. Alter her discount and disount limits for Bob at any time.

#### Views
4. View all allowances targeting her service.

### Remarks 

* On Bob 1.: If Bob contains other allowances for Sarah's service, they will be spend simultanously.  
* On Sarah 2.: Sarah's role is different from Alice's, because Sarah does not transfer tokens to SC. She can offer one discount only, not a portofolio. 

### Example
1. Alice grants an allowance of 9N to Bob to be spend at Sarah's. Alice transfers the coins to SC. Sarah wants to welcome Bob as a customer and adds 1N on top. She does not transfer any coins to SC. She also tells SC that the discount should be at most 10% of the total deal and the minimal size of the deal is 5N. The easy scenario: Bob spends 10N on Sarah's. Sarah receives 9N from SC. No allowance left. More complicated: He spends 6N, 3.4N remain in his allowance. Sarah receives 5.4N.

2. Bob spends 5N at Sarah's on Monday and 5N on Tuesday, out of his wallet. Sarah would like to keep Bob as a customer and gives him a discount of 1N on his next purchase via SC, with no deal limits. Bob can spend the free 1N at Sarah's on Wednesday. But he cannot withdraw the coins from SC. 

3. Bob would like to use Sarah's service frequently. He grants himself an allowance on SC. Sarah gives him a discount to support his plans.   

Benefits
--------
* Alice can make sure Bob spends the money with Sarah's when using SC, compared to a direct transfer. She will choose Sarah's service carefully. 
* Bob can get a better deal with Sarah's compared to just paying directly, because Sarah's service will compete with other services. Bob's wallet remains untouched.  
* Sarah can target new customers and keep regulars by using discounts.    

Problems
--------
* Sarah's service may be reluctant to use SC compared to direct payments from Bob, because it adds cross contract complexity.

Data structure and storage
--------------------------
Bob and Sarah must be known for each transactions. Alice's contributions must be known so that she can withdraw (Actions Alice 2.). 

Approach: One data structure stored on the NEAR blockchain of the following form.
```
{(bob, sarah): [discount, min_deal, max_percentage, {alice: contribution, ...}]}, 
```
where `bob`, `sarah`, `alice` are of type `AccountId`; `discount`, `min_deal`, `contribution` are of type `u128` or `u64`, and `max_percentage` is of type `Percentage`.




