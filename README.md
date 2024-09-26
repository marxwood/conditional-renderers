# Conditional Renderers
```bash
<conditional>
    <if user-is-authenticated>
        <if user-is-admin>
            <switch>
                <case time-is-morning>
                    <render>Good morning</render>
                </case>
                <case time-is-afternoon>
                    <render>Good afternoon</render>
                </case>
                <case time-is-evening>
                    <render>Good evening</render>
                </case>
            </switch>
            <render>{auth.user.name}</render>
        </if>
    </if>
    <else>
        <render>Permisson denied</render>
    </else>
</conditional>
```

If a user by the name John Doe is authenticated and has an admin role, and if the time is morning (03h-12h) the engine should render:
Good morning John Doe.

```bash
<conditional>
    <if user-is-authenticated>
        <if items-exist>
            <render>
                <ul>
                    <li>Item 1</li>
                    <li>Item 2</li>
                    <li>Item 3</li>
                </ul>
            </render>
        </if>
        <else>
            <render>No items</render>
        </else>
    </if>
    <else>
        <render>Permisson denied</render>
    </else>
</conditional>
```

## Tags

### Container

`<conditional>` is a container for conditional logic

### Flow control

`<if>` is a tag that validates a condition. Alternative syntax is `<if condition="name of condition">`
`<else>` is a tag that renders content if no previous `<if>` is fulfilled.
`<else-if>` is a tag that renders content if no previous `<if>` is fulfilled.

`<switch>` is a tag that renders content if the condition is fulfilled.
`<case>` is a tag that renders content if the condition is fulfilled.
`<default>` is a tag that renders content if the condition is fulfilled.
`<break>` is a tag that breaks the switch.

### Rendering

`<render>` can contain any HTML, for example <render><span class="warning">Permission denied.</span></render>.
Consider it a slot within conditional where you put HTML to be rendered in case of fulfilled conditions.
It doesn't make sense to put `<render>` directly inside conditional before validating any conditions. (?)

# Behaviour

Conditional is handled at server-side. It doesn't get to the browser. What gets to the browser is the rendered result after conditional is resolved.
Thus, each `<render>` contained inside the conditional block that validates will be delivered to the browser.

If HTML is broken it will gracefully continue.

# Ideas for server-side flow control based on conditions and other specific features like validating, saving, etc.

```bash
<flow>
    <validate></validate>
    <save></save>
    <render></render>
</flow>```

`<var is-valid="5" />`
