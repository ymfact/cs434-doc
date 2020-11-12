# Out of the Tar Pit

# 3 Approaches to Understanding

The key problem with testing is that a test (of any kind) that uses one particular set of inputs tells you nothing at all about the behaviour of the system or component when it is given a different set of inputs.

Given a stark choice between investment in testing and investment in simplicity, the latter may often be the better choice

# 4 Causes of Complexity

## 4.1 Complexity caused by State

### 4.1.1 Impact of State on Testing

The key problem is that a test (of any kind) on a system or component that is in one particular state tells you nothing at all about the behaviour of that system or component when it happens to be in another state.

### 4.1.2 Impact of State on Informal Reasoning

One of the issues (that affects both testing and reasoning) is the exponential rate at which the number of possible states grows.

Another issue is contamination.

## 4.2 Complexity caused by Control

대부분 언어는 순차 진행하기 때문에, 명령형 로직을 작성하면, 순차적으로 변환되면서 읽기 어려워지고 문제가 생기기 쉽다.

## 4.3 Complexity caused by Code Volume

The final cause of complexity that we want to examine in any detail is sheer code volume.

## 4.4 Other causes of complexity

Complexity breeds complexity.

In the absence of language enforced guarantees (i.e. restrictions on the power of the language)
mistakes (and abuses) will happen.

# 5 Classical approaches to managing complexity

## 5.1 Object-Orientation

### 5.1.1 State

all forms of OOP rely on state (contained within objects) and in general all behaviour is affected by this state.

이 것은 내 경험상 매우 치명적이다. 큰 문제를 가지는 코드를 작성한 뒤에는, 모든 객체를 immutable로 작성하려 노력한다.

## 5.2 Functional Programming

### 5.2.3 Kinds of State

we are using functional values to simulate state.

even though referential transparency is maintained, ease of reasoning is lost.

### 5.2.4 State and Modularity

problems arise when (as is often the case) the system to be built must maintain state of some kind.

# 7 Recommended General Approach

## 7.1 Ideal World

The sole concern when producing the formal requirements must be to ensure that there is no relevant ambiguity in the informal requirements (i.e. that it has no omissions).

### 7.1.1 State in the ideal world

사용자의 요구가 아닌 스테이트는 모두 제거할 수 있다.

사용자의 요구가 아닌 스테이트도 모두 사용자의 요구에서 비롯된 것이며, 언제든 derive할 수 있으므로 전부 스테이트가 아닌 것으로 바꿔버릴 수 있다. (느리겠지만 이상적이라고 가정했으니까.)

### 7.1.2 Control in the ideal world

It typically won’t be mentioned in the informal requirements and hence should not appear in the formal requirements (because these are derived with no view to execution).

## 7.2 Theoretical and Practical Limitations

### 7.2.1 Formal Specification Languages

consideration of specification languages highlights the (theoretically) fuzzy boundary between what is essential and what is accidental

even when specifications are directly executable, this can be impractical for efficiency reasons.

### 7.2.2 Ease of Expression

it can be advantageous to maintain the accidental state even in the ideal world. (the derived data representing the position state of a computer-controlled opponent in an interactive game)

## 7.3 Recommendations

Our recommendations for dealing with complexity (as exemplified by both state and control) can be summed up as:

- Avoid
- Seperate

### 7.3.1 Required Accidental Complexity

Performance: instead we should restrict ourselves to simply declaring what accidental state should be used, and leave it to a completely separate infrastructure (on which our system will eventually run) to maintain.

Ease of Expression: in cases where it really is the only natural thing to do, we should pretend that the accidental state is really essential state for the purposes of the separation discussed below.

### 7.3.2 Separation and the relationship between the components

The first thing that we’re doing is to advocate separating out all complexity of any kind from the pure logic of the system

The second is that we’re further dividing the complexity which we do retain into accidental and essential.

> The logic component determines the meaning ... whereas the control component only affects its efficiency.

A consequence of separation is that the separately specified components will each be of a very different nature, and as a result it may be ideal to use different languages for each.

The vital importance of separation comes simply from the fact that it is separation that allows us to “restrict the power” of each of the components independently.

Changes in the accidental specification can hence never require any change to the essential logic.
