# 添加自定义卡片

```tsx
import React from "react";
import { Plugin, SchemaSettings, useSchemaInitializer } from "@tachybase/client";
import { ISchema } from "@tachybase/schema";

// AI 卡片
export const AiChatBlock = () => {
  return <div>this is my ai chat card</div>;
};


// 卡片配置
export const aiChatSettings = new SchemaSettings({
    name: `blockSettings:aiChatBlock`,
    items: [
      {
        type: 'remove',
        name: 'remove',
        componentProps: {
          removeParentsIfNoChildren: true,
          breakRemoveOn: {
            'x-component': 'Grid',
          },
        }
      }
    ]
  });

// 卡片 schema
export const aiChatSchema: ISchema = {
  type: "void",
  "x-component": "CardItem",
  'x-settings': aiChatSettings.name,
  properties: {
    aiChatBlock: {
      "x-component": "AiChatBlock",
    },
  },
};

// 添加 卡片的选项配置
const aiChatBlockItem = {
  type: "item",
  name: "aiChartBlock",
  icon: "FileImageOutlined",
  useComponentProps() {
    const { insert } = useSchemaInitializer();
    return {
      title: "ai chat",
      onClick() {
        insert(aiChatSchema);
      },
    };
  },
};

export class PluginDemoCard extends Plugin {
  async load() {
    this.app.addComponents({ AiChatBlock }); // 注册卡片
    this.app.schemaSettingsManager.add(aiChatSettings);
    this.app.schemaInitializerManager.addItem(
      "page:addBlock",
      `otherBlocks.aiChatBlock`,
      aiChatBlockItem
    ); // 注册到卡片生成器中
  }
}

```