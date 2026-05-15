# Container-Presenter-Pattern

![img](/images/containerPresenterPattern.png)

- We will create a **_Container Component_**.
- A Container Component is all about fetching data and managing the data.
- A Container Component will never ever deal with Presentation Part(the UI)
- The **_Presenter Component_** might get bigger so we will create more Sub-Presenter Components.
- Overall: Container Component will fetch the data and give it to Presenter Component and the Presenter Component will slice and dice the data to Show the User.

---

## Use Cases

1. Perfect for Component that fetch data/APIs
2. Real time Data display
3. User Dashboard
4. Form heavy application
5. Checkout Process
6. Survey forms

## Pitfall

1. Don't over engineer simple components
2. If the layer of sub presenter components are too many . for example , We need to send 10-15 props to one presenter component then those will go sub component and again sub sub component then it will get too messy again. we will use this _Container-Presenter-Pattern_ patten when the component layer will be max 3 level.other wise we will use another **Design Patter** which is called _Context Design Pattern_.

## example:

![exp](/images/ContainerPresenterVisual.png)
[text](https://)
