#### Kubernetes infrastructure in the UI

Starting in 2.26, the UI has been updated to more closely follow immutable infrastructure principles. When you navigate to the **Infrastructure** tab in the UI for an application that has the Kubernetes provider configured, you no longer see actions, such as **Create** or **Delete**, for the Kubernetes infrastructure, including Clusters, Load Balancers, and Firewalls.

**Impact**

Users no longer see these actions in the UI.

**Workaround**

Instead of being available by default, whether or not these actions are available in the UI is now controlled by the following property in `settings-local.yml`:

```yaml
window.spinnakerSettings.kubernetesAdHocInfraWritesEnabled = <boolean>;
```

This property affects only Kubernetes infrastructure. The behavior is slightly different depending on if the application has only the Kubernetes provider or Kubernetes and other providers, such as AWS.

If the application only has the Kubernetes provider configured, the following applies:

- When set to `true`, this property causes the UI to function as it did in previous releases. This allows people to manually create and delete Kubernetes infrastructure from the UI.
- When set to `false`, this property causes the actions to be unavailable to users. This prevents users from manually creating and deleting Kubernetes infrastructure from the UI. The users can still view the infrastructure but cannot make changes through the UI.

If the application includes Kubernetes and other providers, the following applies:

- When set to `true`, this property causes the UI to function as it did in previous releases. This allows people to manually create and delete Kubernetes infrastructure from the UI. Users can continue to select whether they want to create Kubernetes or other infrastructure in the UI.
- When set to `false`, this property causes Kubernetes to be unavailable as an option when trying to modify infrastructure from the UI. Users can still make changes to infrastructure for the application from cloud providers, such as AWS, but not Kubernetes.

**Introduced in**: Armory 2.26.0