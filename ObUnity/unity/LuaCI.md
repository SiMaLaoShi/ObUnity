```lua
local https = require("ssl.https")
local ltn12 = require("ltn12")
local json = require("cjson")
local webhook = ""

local function send_dingtalk_message(msgtype, message)
    local response_body = {}
    local payload = json.encode(message)

    local result, response_code, response_headers, response_status_line = https.request{
        url = webhook,
        method = "POST",
        headers = {
            ["Content-Type"] = "application/json;charset=utf-8",
            ["Content-Length"] = #payload
        },
        source = ltn12.source.string(payload),
        sink = ltn12.sink.table(response_body),
        protocol = "tlsv1_2"
    }
    
    print("Status code:", response_code)
    print("Response body:", table.concat(response_body))
end

-- 发送 Markdown 消息
local markdown_msg = {
    msgtype = "markdown",
    markdown = {
        title = "",
        text = "",
    },
    at = {}
}

function send_dingtalk_markdown(text)
    markdown_msg.markdown.text = text
    send_dingtalk_message("markdown", markdown_msg)
end

function is_directory_exists(path)
    local attributes = lfs.attributes(path) -- 获取路径的属性
    return attributes and attributes.mode == "directory" -- 检查是否为文件夹
end

function generate_qr_code(data, output_file)
    -- 确保data没有引号或其他特殊字符，可能需要额外的转义处理
    -- output_file是你想要保存二维码图像的文件路径
    local command = string.format('qrencode -o %s %s', output_file, data)
    local success = os.execute(command)
    if not success then
        app.send_log("QR code generation failed")
        return false;
    end
    return true
end

local function replace_dots_and_dashes(input_str)
    local result = input_str
    -- 使用 % 替换特殊字符 . 和 - ，因为它们在 Lua 的模式匹配中有特殊含义
    result = result:gsub('%.', '_') -- 将 . 替换为 _
    result = result:gsub('%-', '_') -- 将 - 替换为 _
    return result
end

function generate_install_html(qr_code, new_app_name, new_app_url, dest_html)
	local original_html, err = read_html("install_temple.html")
	if not original_html then
	    print(err)
	    return false
	end

	-- 替换图片、应用名称、应用链接
	local updated_html = replace_content(original_html, qr_code, new_app_name, new_app_url)

	-- 将修改后的 HTML 写入同一个文件或新文件
	local result, err = write_html(dest_html, updated_html)
	if not result then
	    print(err)
	    return false
	end
	return true
end

function replace_content(original_html, qr_code, new_app_name, new_app_url)
    local modified_html = original_html
    modified_html = modified_html:gsub('QR_SRC', qr_code) -- 替换图片路径
    modified_html = modified_html:gsub('APP_NAME', new_app_name) -- 替换应用名称
    modified_html = modified_html:gsub('APP_LINK', new_app_url) -- 替换应用链接
    return modified_html
end
```
lua打包通知钉钉机器人

```sh
brew install openssl
brew update --auto-update
brew install qrencode
brew install luarocks
luarocks install lua-cjson
luarocks install luasec
luarocks install luasocket

```
环境配置