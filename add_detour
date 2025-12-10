// 落地节点自动 detour（后处理脚本）
// 用法：放在 sing-box/template.js 之后执行

const parser = (typeof ProxyUtils !== 'undefined' && ProxyUtils.JSON5) || JSON

log('开始：为包含“落地”的节点添加 detour')

let config
try {
  config = parser.parse($content ?? $files?.[0])
} catch (e) {
  throw new Error('配置文件不是合法 JSON：' + (e?.message || e))
}

if (Array.isArray(config.outbounds)) {
  config.outbounds.forEach(ob => {
    const tag = ob.tag || ''

    // 只给“节点”加，不给 selector/url-test 这些分组加
    const groupTypes = ['selector', 'urltest', 'url-test', 'fallback', 'direct', 'block']

    if (tag.includes('落地') && !groupTypes.includes(ob.type)) {
      ob.detour = '🚀 节点选择'
    }
  })
}

$content = JSON.stringify(config, null, 2)

function log(msg) {
  console.log('[落地-detour] ' + msg)
}
