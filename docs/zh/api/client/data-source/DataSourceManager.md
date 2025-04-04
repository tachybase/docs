# DataSourceManager

数据源管理器,用于管理 `DataSource` 实例。

## 1. 实例属性

### collectionTemplateManager

用于管理 `CollectionTemplate` 实例。

```tsx | pure
import { Plugin, CollectionTemplate } from '@tachybase/client'

class MyCollectionTemplate extends CollectionTemplate {
  name = 'my-collection-template'
}

class MyPlugin extends Plugin {
  async load() {
    this.app.dataSourceManager.collectionTemplateManager.addCollectionTemplates([
      MyCollectionTemplate,
    ])
  }
}
```

详细请参考：[CollectionTemplateManager](./CollectionTemplateManager)

### collectionFieldInterfaceManager

用于管理 `CollectionFieldInterface` 实例。

```tsx | pure
import { Plugin, CollectionFieldInterface } from '@tachybase/client'

class MyCollectionFieldInterface extends CollectionFieldInterface {
  name = 'my-collection-field-interface'
}

class MyPlugin extends Plugin {
  async load() {
    this.app.dataSourceManager.collectionFieldInterfaceManager.addFieldInterfaces([
      MyCollectionFieldInterface,
    ])
  }
}
```

详细请参考：[CollectionFieldInterfaceManager](./CollectionFieldInterfaceManager)

## 2. 实例方法

### addCollectionTemplates()

是 `CollectionTemplateManager` 的快捷方法，用于添加 `CollectionTemplate`。

- 类型

```tsx | pure
class DataSourceManager {
  addCollectionTemplates(templates: CollectionTemplate[]): void
}
```

- 示例

```tsx | pure
import { Plugin, CollectionTemplate } from '@tachybase/client'

class MyCollectionTemplate extends CollectionTemplate {
  name = 'my-collection-template'
}

class MyPlugin extends Plugin {
  async load() {
    this.app.dataSourceManager.collectionTemplateManager.addCollectionTemplates([
      MyCollectionTemplate,
    ])
  }
}
```

更多详细请参考：[CollectionTemplateManager](./CollectionTemplateManager)

### addFieldInterfaces()

是 `CollectionFieldInterfaceManager` 的快捷方法，用于添加 `CollectionFieldInterface`。

- 类型

```tsx | pure
class DataSourceManager {
  addFieldInterfaces(fieldInterfaces: CollectionFieldInterface[]): void
}
```

- 示例

```tsx | pure
import { Plugin, CollectionFieldInterface } from '@tachybase/client'

class MyCollectionFieldInterface extends CollectionFieldInterface {
  name = 'my-collection-field-interface'
}

class MyPlugin extends Plugin {
  async load() {
    this.app.dataSourceManager.collectionFieldInterfaceManager.addFieldInterfaces([
      MyCollectionFieldInterface,
    ])
  }
}
```

更多详细请参考：[CollectionFieldInterfaceManager](./CollectionFieldInterfaceManager)

### addCollectionMixins()

用于添加 `Collection` 的 Mixins。

- 类型

```tsx | pure
class DataSourceManager {
  addCollectionMixins(mixins: (typeof Collection)[]): void
}
```

- 示例

```tsx | pure
import { Plugin, Collection } from '@tachybase/client'

class MyCollectionMixin extends Collection {
  otherMethod() {
    console.log('otherMethod')
  }
}

class MyPlugin extends Plugin {
  async load() {
    this.app.dataSourceManager.addCollectionMixins([MyCollectionMixin])
  }
}

const MyComponent = () => {
  const collection = useCollection<MyCollectionMixin>()
  collection.otherMethod()
}
```

更多详细请参考：[CollectionMixins](./CollectionMixins)

### addDataSource()

用于添加 `DataSource`。

- 类型

```tsx | pure
class DataSourceManager {
  addDataSource(DataSource: DataSource, options: DataSourceOptions): void
}
```

- 示例

```tsx | pure
import { Plugin, DataSource, DataSourceOptions } from '@tachybase/client'

class MyDataSource extends DataSource {
  async getDataSource() {
    return {
      status: 'loaded',
      collections: [{ name: 'users' }],
    }
  }
}

class MyPlugin extends Plugin {
  async load() {
    this.app.dataSourceManager.addDataSource(MyDataSource, {
      key: 'my-data-source',
      displayName: 'My Data Source',
    })
  }
}
```

更多详细请参考：[DataSource](./DataSource)

### removeDataSources()

移除 `DataSource`。

- 类型

```tsx | pure
class DataSourceManager {
  removeDataSources(keys: string[]): void
}
```

- 示例

```tsx | pure
const MyComponent = () => {
  const dataSourceManager = useDataSourceManager()
  dataSourceManager.removeDataSources(['my-data-source'])
}
```

### getDataSources()

获取全部 `DataSource` 实例列表。

- 类型

```tsx | pure
class DataSourceManager {
  getDataSources(): DataSource[]
}
```

- 示例

```tsx | pure
const MyComponent = () => {
  const dataSourceManager = useDataSourceManager()
  const dataSources = dataSourceManager.getDataSources()

  return (
    <div>
      {dataSources.map(dataSource => (
        <div key={dataSource.key}>{dataSource.displayName}</div>
      ))}
    </div>
  )
}
```

### getDataSource(key)

获取 `DataSource` 实例。

- 类型

```tsx | pure
class DataSourceManager {
  getDataSource(key: string): DataSource
}
```

- 示例

```tsx | pure
const MyComponent = () => {
  const dataSourceManager = useDataSourceManager()
  const dataSource = dataSourceManager.getDataSource('my-data-source')

  return <div>{dataSource.displayName}</div>
}
```

### getAllCollections()

获取所有 DataSource 的所有 Collection 实例。

- 类型

```tsx | pure
class DataSourceManager {
  getAllCollections(options?: {
    filterCollection?: (collection: Collection) => boolean
    filterDataSource?: (dataSource: DataSource) => boolean
  }): (DataSourceOptions & { collections: Collection[] })[]
}
```

- 示例

```tsx | pure
const MyComponent = () => {
  const dataSourceManager = useDataSourceManager()
  const collections = dataSourceManager.getAllCollections()

  return (
    <div>
      {collections.map(({ key, displayName, collections }) => (
        <div key={key}>
          <h3>{displayName}</h3>
          <ul>
            {collections.map(collection => (
              <li key={collection.name}>{collection.name}</li>
            ))}
          </ul>
        </div>
      ))}
    </div>
  )
}
```

### reload()

重载所有 `DataSource`。

- 类型

```tsx | pure
class DataSourceManager {
  reload(): Promise<void>
}
```

- 示例

```tsx | pure
const MyComponent = () => {
  const dataSourceManager = useDataSourceManager()
  dataSourceManager.reload()
}
```
