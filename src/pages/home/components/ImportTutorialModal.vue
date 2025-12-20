<script setup lang="ts">
import { ref } from 'vue'

// Props
defineProps<{
  open: boolean
}>()

// Emits
const emit = defineEmits<{
  'update:open': [value: boolean]
}>()

// 通用格式弹窗状态
const showFormatModal = ref(false)

// 复制格式示例（完整版）
const formatExample = `{
  "chatlab": {
    "version": "0.0.1",
    "exportedAt": 1732924800,
    "generator": "Your Tool Name",
    "description": "自定义描述信息"
  },
  "meta": {
    "name": "群聊名称",
    "platform": "qq",
    "type": "group",
    "groupId": "123456789",
    "groupAvatar": "data:image/jpeg;base64,/9j/4AAQ..."
  },
  "members": [
    {
      "platformId": "123456789",
      "accountName": "用户昵称",
      "groupNickname": "群昵称（可选）",
      "avatar": "data:image/jpeg;base64,/9j/4AAQ..."
    }
  ],
  "messages": [
    {
      "sender": "123456789",
      "accountName": "发送时昵称",
      "groupNickname": "发送时群昵称（可选）",
      "timestamp": 1732924800,
      "type": 0,
      "content": "消息内容"
    }
  ]
}`

function copyFormatExample() {
  navigator.clipboard.writeText(formatExample)
}

function closeModal() {
  emit('update:open', false)
}

function openExternalLink(url: string) {
  window.open(url, '_blank')
}
</script>

<template>
  <!-- 导入教程弹窗 -->
  <UModal :open="open" @update:open="emit('update:open', $event)" :ui="{ content: 'md:w-full max-w-2xl' }">
    <template #content>
      <div class="p-6">
        <!-- Header -->
        <div class="mb-6 flex items-center justify-between">
          <div class="flex items-center gap-3">
            <div
              class="flex h-10 w-10 items-center justify-center rounded-xl bg-linear-to-br from-pink-100 to-rose-100 dark:from-pink-900/30 dark:to-rose-900/30"
            >
              <UIcon name="i-heroicons-book-open" class="h-5 w-5 text-pink-600 dark:text-pink-400" />
            </div>
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">聊天记录导入教程</h2>
          </div>
          <UButton icon="i-heroicons-x-mark" variant="ghost" size="sm" @click="closeModal" />
        </div>

        <!-- 教程内容 -->
        <div class="space-y-6">
          <!-- QQ 教程 -->
          <div class="rounded-xl border border-gray-200 p-4 dark:border-gray-700">
            <div class="mb-3 flex items-center gap-2">
              <UIcon name="i-heroicons-chat-bubble-left-right" class="h-5 w-5 text-pink-500" />
              <h3 class="font-semibold text-gray-900 dark:text-white">QQ</h3>
            </div>
            <ol class="space-y-2">
              <li class="flex items-start gap-3 text-sm text-gray-600 dark:text-gray-300">
                <span
                  class="flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-pink-100 text-xs font-medium text-pink-600 dark:bg-pink-900/30 dark:text-pink-400"
                >
                  1
                </span>
                <span>
                  使用
                  <a
                    class="cursor-pointer text-pink-600 underline underline-offset-2 hover:text-pink-700 dark:text-pink-400 dark:hover:text-pink-300"
                    @click="openExternalLink('https://github.com/shuakami/qq-chat-exporter')"
                  >
                    qq-chat-exporter
                    <UIcon name="i-heroicons-arrow-top-right-on-square" class="inline h-3 w-3" />
                  </a>
                  导出聊天记录（目前仅支持Windows/Linux）
                </span>
              </li>
              <li class="flex items-start gap-3 text-sm text-gray-600 dark:text-gray-300">
                <span
                  class="flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-pink-100 text-xs font-medium text-pink-600 dark:bg-pink-900/30 dark:text-pink-400"
                >
                  2
                </span>
                <span>导出完成后会得到 .json 或 .jsonl 文件</span>
              </li>
              <li class="flex items-start gap-3 text-sm text-gray-600 dark:text-gray-300">
                <span
                  class="flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-pink-100 text-xs font-medium text-pink-600 dark:bg-pink-900/30 dark:text-pink-400"
                >
                  3
                </span>
                <span>将文件拖拽到上方导入区域</span>
              </li>
            </ol>
          </div>

          <!-- 微信教程 -->
          <div class="rounded-xl border border-gray-200 p-4 dark:border-gray-700">
            <div class="mb-3 flex items-center gap-2">
              <UIcon name="i-heroicons-device-phone-mobile" class="h-5 w-5 text-blue-500" />
              <h3 class="font-semibold text-gray-900 dark:text-white">微信或其他聊天应用</h3>
            </div>
            <ol class="mb-4 space-y-2">
              <li class="flex items-start gap-3 text-sm text-gray-600 dark:text-gray-300">
                <span
                  class="flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-blue-100 text-xs font-medium text-blue-600 dark:bg-blue-900/30 dark:text-blue-400"
                >
                  1
                </span>
                <span>Github上有很多开源的导出工具，请自行找工具导出微信等软件的聊天记录</span>
              </li>
              <li class="flex items-start gap-3 text-sm text-gray-600 dark:text-gray-300">
                <span
                  class="flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-blue-100 text-xs font-medium text-blue-600 dark:bg-blue-900/30 dark:text-blue-400"
                >
                  2
                </span>
                <span>使用脚本，将导出文件转换为 ChatLab 通用格式</span>
              </li>
              <li class="flex items-start gap-3 text-sm text-gray-600 dark:text-gray-300">
                <span
                  class="flex h-5 w-5 shrink-0 items-center justify-center rounded-full bg-blue-100 text-xs font-medium text-blue-600 dark:bg-blue-900/30 dark:text-blue-400"
                >
                  3
                </span>
                <span>将转换后的 .json 或 .jsonl 文件拖拽到上方导入区域</span>
              </li>
            </ol>
            <UButton
              variant="soft"
              size="sm"
              :trailing-icon="'i-heroicons-document-text'"
              @click="showFormatModal = true"
            >
              查看通用格式说明
            </UButton>
          </div>
        </div>

        <!-- 底部提示 -->
        <div class="mt-6 rounded-lg bg-gray-50 p-4 dark:bg-gray-800/50">
          <p class="text-sm text-gray-500 dark:text-gray-400">
            💡 提示：ChatLab 支持多种聊天记录格式（.json、.jsonl、.txt），包括 QQ、微信、Discord
            等平台。将导出的文件直接拖拽到导入区域即可开始分析。
          </p>
          <p class="mt-2 text-xs text-gray-400 dark:text-gray-500">
            📦 对于超大规模聊天记录（>100万条），建议使用 JSONL 格式，可避免内存溢出问题。
          </p>
        </div>
      </div>
    </template>
  </UModal>

  <!-- 通用格式说明弹窗（层级高于教程弹窗） -->
  <UModal v-model:open="showFormatModal" :ui="{ content: 'md:w-full max-w-3xl z-[60]', overlay: 'z-[60]' }">
    <template #content>
      <div class="p-6">
        <!-- Header -->
        <div class="mb-6 flex items-center justify-between">
          <div class="flex items-center gap-3">
            <div
              class="flex h-10 w-10 items-center justify-center rounded-xl bg-linear-to-br from-blue-100 to-indigo-100 dark:from-blue-900/30 dark:to-indigo-900/30"
            >
              <UIcon name="i-heroicons-document-text" class="h-5 w-5 text-blue-600 dark:text-blue-400" />
            </div>
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">ChatLab 通用格式说明</h2>
          </div>
          <UButton icon="i-heroicons-x-mark" variant="ghost" size="sm" @click="showFormatModal = false" />
        </div>

        <!-- 格式说明 -->
        <div class="max-h-[60vh] space-y-4 overflow-y-auto">
          <p class="text-sm text-gray-600 dark:text-gray-300">
            ChatLab 定义了一套聊天记录分析用标准格式，支持两种文件格式。只需在文件中包含
            <code class="rounded bg-gray-100 px-1.5 py-0.5 text-pink-600 dark:bg-gray-800 dark:text-pink-400">
              chatlab
            </code>
            对象即可被识别。
          </p>

          <!-- 格式对比说明 -->
          <div class="rounded-lg bg-gray-50 p-3 dark:bg-gray-800/50">
            <div class="mb-2 text-xs font-medium text-gray-500 dark:text-gray-400">支持的格式</div>
            <div class="flex gap-4 text-xs">
              <div class="flex items-center gap-2">
                <span class="rounded bg-gray-200 px-2 py-0.5 font-mono dark:bg-gray-700">.json</span>
                <span class="text-gray-600 dark:text-gray-300">标准格式，适合中小型记录</span>
              </div>
              <div class="flex items-center gap-2">
                <span
                  class="rounded bg-blue-100 px-2 py-0.5 font-mono text-blue-700 dark:bg-blue-900/50 dark:text-blue-300"
                >
                  .jsonl
                </span>
                <span class="text-gray-600 dark:text-gray-300">流式格式，支持 GB 级超大文件</span>
              </div>
            </div>
          </div>

          <p class="text-xs text-gray-500 dark:text-gray-400">
            以下是 JSON 格式规范示例。JSONL 格式规范请参考
            <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">.docs/guide/chatLabJsonlFormat.md</code>
          </p>

          <!-- JSON 示例 -->
          <div class="rounded-xl border border-gray-200 bg-gray-50 p-4 dark:border-gray-700 dark:bg-gray-800/50">
            <div class="mb-2 flex items-center justify-between">
              <span class="text-xs font-medium text-gray-500 dark:text-gray-400">完整示例（含可选字段）</span>
              <UButton variant="ghost" size="xs" icon="i-heroicons-clipboard-document" @click="copyFormatExample">
                复制
              </UButton>
            </div>
            <pre class="overflow-x-auto text-xs leading-relaxed text-gray-700 dark:text-gray-300"><code>{
  "chatlab": {
    "version": "0.0.1",           // 必填：格式版本号
    "exportedAt": 1732924800,     // 必填：导出时间（秒级时间戳）
    "generator": "Your Tool Name", // 可选：生成工具名称
    "description": "自定义描述"    // 可选：描述信息（自定义内容）
  },
  "meta": {
    "name": "群聊名称",            // 必填：群名/对话名
    "platform": "qq",             // 必填：qq | wechat | discord | mixed | unknown 等
    "type": "group",              // 必填：group（群聊）| private（私聊）
    "groupId": "123456789",       // 可选：群ID（仅群聊）
    "groupAvatar": "data:image/jpeg;base64,..." // 可选：群头像（Data URL）
  },
  "members": [
    {
      "platformId": "123456789",  // 必填：用户唯一标识（QQ号/微信ID等）
      "accountName": "用户昵称",   // 必填：账号名称
      "groupNickname": "群昵称",   // 可选：群昵称（仅群聊）
      "avatar": "data:image/jpeg;base64,..." // 可选：用户头像（Data URL）
    }
  ],
  "messages": [
    {
      "sender": "123456789",      // 必填：发送者 platformId
      "accountName": "发送时昵称", // 必填：发送时的账号名称
      "groupNickname": "发送时群昵称", // 可选：发送时的群昵称
      "timestamp": 1732924800,    // 必填：秒级 Unix 时间戳
      "type": 0,                  // 必填：消息类型（见下方说明，0=文本）
      "content": "消息内容"        // 必填：消息内容（null 表示非文本）
    }
  ]
}</code></pre>
          </div>

          <!-- 消息类型说明 -->
          <div class="rounded-xl border border-gray-200 bg-white p-4 dark:border-gray-700 dark:bg-gray-800">
            <h3 class="mb-3 text-sm font-semibold text-gray-900 dark:text-white">消息类型 (type)</h3>

            <!-- 基础类型 (0-19) -->
            <p class="mb-2 text-xs font-medium text-gray-500 dark:text-gray-400">基础消息类型 (0-19)</p>
            <div class="mb-3 grid grid-cols-2 gap-2 text-xs sm:grid-cols-4">
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">0</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">TEXT 文本</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">1</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">IMAGE 图片</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">2</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">VOICE 语音</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">3</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">VIDEO 视频</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">4</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">FILE 文件</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">5</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">EMOJI 表情</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">7</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">LINK 链接</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">8</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">LOCATION 位置</span>
              </div>
            </div>

            <!-- 交互类型 (20-39) -->
            <p class="mb-2 text-xs font-medium text-gray-500 dark:text-gray-400">交互消息类型 (20-39)</p>
            <div class="mb-3 grid grid-cols-2 gap-2 text-xs sm:grid-cols-4">
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">20</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">RED_PACKET 红包</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">21</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">TRANSFER 转账</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">22</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">POKE 拍一拍</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">23</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">CALL 通话</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">24</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">SHARE 分享</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">25</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">REPLY 回复</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">26</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">FORWARD 转发</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">27</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">CONTACT 名片</span>
              </div>
            </div>

            <!-- 系统/其他 (80+) -->
            <p class="mb-2 text-xs font-medium text-gray-500 dark:text-gray-400">系统消息类型 (80+)</p>
            <div class="grid grid-cols-2 gap-2 text-xs sm:grid-cols-4">
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">80</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">SYSTEM 系统</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">81</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">RECALL 撤回</span>
              </div>
              <div class="rounded-lg bg-gray-50 p-2 dark:bg-gray-700">
                <span class="font-mono text-pink-600 dark:text-pink-400">99</span>
                <span class="ml-2 text-gray-600 dark:text-gray-300">OTHER 其他</span>
              </div>
            </div>
          </div>

          <!-- 头像格式说明 -->
          <div class="rounded-xl border border-gray-200 bg-white p-4 dark:border-gray-700 dark:bg-gray-800">
            <h3 class="mb-3 text-sm font-semibold text-gray-900 dark:text-white">头像格式说明</h3>
            <p class="mb-2 text-xs text-gray-600 dark:text-gray-300">
              头像字段（
              <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">avatar</code>
              、
              <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">groupAvatar</code>
              ）使用 Data URL 格式：
            </p>
            <pre
              class="mb-3 overflow-x-auto rounded-lg bg-gray-50 p-2 text-xs text-gray-700 dark:bg-gray-700 dark:text-gray-300"
            ><code>data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD...</code></pre>
            <p class="text-xs text-gray-500 dark:text-gray-400">
              支持的 MIME 类型：
              <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">image/jpeg</code>
              、
              <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">image/png</code>
              、
              <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">image/gif</code>
              、
              <code class="rounded bg-gray-100 px-1 dark:bg-gray-700">image/webp</code>
            </p>
            <p class="text-xs text-gray-500 dark:text-gray-400">建议导出时压缩处理，100*100像素即可满足需求</p>
          </div>

          <!-- 字段必要性 -->
          <div class="rounded-xl border border-gray-200 bg-white p-4 dark:border-gray-700 dark:bg-gray-800">
            <h3 class="mb-3 text-sm font-semibold text-gray-900 dark:text-white">字段必要性速查</h3>
            <div class="grid grid-cols-1 gap-3 text-xs sm:grid-cols-2">
              <div>
                <h4 class="mb-2 font-medium text-gray-700 dark:text-gray-300">✅ 必填字段</h4>
                <ul class="space-y-1 text-gray-600 dark:text-gray-400">
                  <li><code class="rounded bg-green-50 px-1 dark:bg-green-900/30">chatlab.version</code></li>
                  <li><code class="rounded bg-green-50 px-1 dark:bg-green-900/30">chatlab.exportedAt</code></li>
                  <li>
                    <code class="rounded bg-green-50 px-1 dark:bg-green-900/30">meta.name / platform / type</code>
                  </li>
                  <li>
                    <code class="rounded bg-green-50 px-1 dark:bg-green-900/30">
                      members[].platformId / accountName
                    </code>
                  </li>
                  <li><code class="rounded bg-green-50 px-1 dark:bg-green-900/30">messages[] 所有基础字段</code></li>
                </ul>
              </div>
              <div>
                <h4 class="mb-2 font-medium text-gray-700 dark:text-gray-300">📎 可选字段</h4>
                <ul class="space-y-1 text-gray-600 dark:text-gray-400">
                  <li>
                    <code class="rounded bg-blue-50 px-1 dark:bg-blue-900/30">chatlab.generator / description</code>
                  </li>
                  <li><code class="rounded bg-blue-50 px-1 dark:bg-blue-900/30">meta.groupId / groupAvatar</code></li>
                  <li>
                    <code class="rounded bg-blue-50 px-1 dark:bg-blue-900/30">members[].groupNickname / avatar</code>
                  </li>
                  <li><code class="rounded bg-blue-50 px-1 dark:bg-blue-900/30">messages[].groupNickname</code></li>
                </ul>
              </div>
            </div>
          </div>
        </div>

        <!-- 底部提示 -->
        <div class="mt-6 space-y-2 rounded-lg bg-blue-50 p-4 dark:bg-blue-900/20">
          <p class="text-sm text-blue-600 dark:text-blue-400">
            💡 文件名以
            <code class="rounded bg-blue-100 px-1 dark:bg-blue-800">.json</code>
            或
            <code class="rounded bg-blue-100 px-1 dark:bg-blue-800">.jsonl</code>
            结尾，包含
            <code class="rounded bg-blue-100 px-1 dark:bg-blue-800">chatlab</code>
            对象即可被识别。
          </p>
          <p class="text-xs text-blue-500 dark:text-blue-400/80">
            📖 JSON 格式规范：
            <code class="rounded bg-blue-100 px-1 dark:bg-blue-800">.docs/guide/chatLabFormat.md</code>
          </p>
          <p class="text-xs text-blue-500 dark:text-blue-400/80">
            📖 JSONL 格式规范：
            <code class="rounded bg-blue-100 px-1 dark:bg-blue-800">.docs/guide/chatLabJsonlFormat.md</code>
          </p>
        </div>
      </div>
    </template>
  </UModal>
</template>
