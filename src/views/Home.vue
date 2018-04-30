<template>
    <my-page title="CSS 库">
        <ui-select-field class="select" v-model="style" label="选择样式">
            <ui-menu-item :value="item.link" :title="item.name" v-for="item in styles" :key="item.name"/>
        </ui-select-field>
        <article class="article ui-article markdown-body">
            <h1>一级标题</h1>
            <h2>二级标题</h2>
            <h3>三级标题</h3>
            <h4>四级标题</h4>
            <h5>五级标题</h5>
            <h6>六级标题</h6>
            <p>这是一个很普通的段落，很普通很普通很普通很普通很普通很普通很普通很普通很普通很普通的段落。</p>
            <p>Now is the time for all good men to come to
            the aid of their country. This is just a
            regular paragraph.</p>
            <p>The quick brown fox jumped over the lazy
            dog&#39;s back.</p>
            <hr>
            <h3>Header 3</h3>
            <blockquote>
            <p>This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
            consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
            Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.</p>
            <p>Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
            id sem consectetuer libero luctus adipiscing.</p>
            <h2>This is an H2 in a blockquote</h2>
            <p>This is the first level of quoting.</p>
            <blockquote>
            <p>This is nested blockquote.</p>
            </blockquote>
            <p>Back to the first level.</p>
            </blockquote>
            <p>Some of these words <em>are emphasized</em>.
            Some of these words <em>are emphasized also</em>.</p>
            <p>Use two asterisks for <strong>strong emphasis</strong>.
            Or, if you prefer, <strong>use two underscores instead</strong>.</p>
            <ul>
            <li>Candy.</li>
            <li>Gum.</li>
            <li>Booze.</li>
            <li>Red</li>
            <li>Green</li>
            <li><p>Blue</p>
            </li>
            <li><p>A list item.</p>
            </li>
            </ul>
            <p>With multiple paragraphs.</p>
            <ul>
            <li><p>Another item in the list.</p>
            </li>
            <li><p>This is a list item with two paragraphs. Lorem ipsum dolor
            sit amet, consectetuer adipiscing elit. Aliquam hendrerit
            mi posuere lectus.</p>
            </li>
            </ul>
            <p>Vestibulum enim wisi, viverra nec, fringilla in, laoreet
            vitae, risus. Donec sit amet nisl. Aliquam semper ipsum
            sit amet velit.*   Suspendisse id sem consectetuer libero luctus adipiscing.</p>
            <ul>
            <li>This is a list item with two paragraphs.</li>
            </ul>
            <p>This is the second paragraph in the list item. You&#39;re
            only required to indent the first line. Lorem ipsum dolor
            sit amet, consectetuer adipiscing elit.</p>
            <ul>
            <li><p>Another item in the same list.</p>
            </li>
            <li><p>A list item with a bit of <code>code</code> inline.</p>
            </li>
            <li><p>A list item with a blockquote:</p>
            <blockquote>
            <p>This is a blockquote
            inside a list item.</p>
            </blockquote>
            </li>
            </ul>
            <p>接着，测试一下有序列表的显示效果：</p>
            <ol>
            <li>有序列表项。</li>
            <li>有序列表项。</li>
            <li>有序列表项。</li>
            <li>有序列表项。</li>
            </ol>
            <p>测试一下表格的显示效果：</p>
            <table>
            <thead>
            <tr>
            <th>水果</th>
            <th style="text-align:center">价格</th>
            <th style="text-align:center">数量</th>
            </tr>
            </thead>
            <tbody>
            <tr>
            <td>香蕉</td>
            <td style="text-align:center">$1</td>
            <td style="text-align:center">5</td>
            </tr>
            <tr>
            <td>苹果</td>
            <td style="text-align:center">$1</td>
            <td style="text-align:center">6</td>
            </tr>
            <tr>
            <td>草莓</td>
            <td style="text-align:center">$1</td>
            <td style="text-align:center">7</td>
            </tr>
            </tbody>
            </table>
            <p>Here is an example of a pre code block</p>
            <pre><code>tell application &quot;Foo&quot;
                beep
            end tell
            </code></pre><p>再测试一下代码的样式：</p>
            <pre><code class="lang-javascript">console.log(&#39;hello world&#39;)
            </code></pre>
            <p>This is an <a href="http://example.com/">example link</a>.</p>
            <p>I get 10 times more traffic from <a href="http://google.com/" title="Google">Google</a> than from
            <a href="http://search.yahoo.com/" title="Yahoo Search">Yahoo</a> or <a href="http://search.msn.com/" title="MSN Search">MSN</a>.</p>
            <p>I start my morning with a cup of coffee and
            <a href="http://www.nytimes.com/">The New York Times</a>.</p>

        </article>
    </my-page>
</template>

<script>
    export default {
        data () {
            return {
                style: '/static/md1.css',
                styles: [
                    {
                        name: 'Github mardown css',
                        link: '/static/md1.css'
                    },
                    {
                        name: '测试样式',
                        link: '/static/md2.css'
                    },
                    {
                        name: 'Dark',
                        link: '/static/md3.css'
                    }
                ],
                page: {
                    menu: [
                        {
                            type: 'icon',
                            icon: 'help',
                            to: '/help'
                        }
                    ]
                }
            }
        },
        mounted() {
            this.init()
        },
        methods: {
            init() {
                this.loadStyle()
                this.initWebIntents()
            },
            initWebIntents() {
                if (!window.intent) {
                    return
                }
                this.page.menu.push({
                    type: 'icon',
                    icon: 'check',
                    click: this.finish,
                    title: '完成'
                })
            },
            finish() {
                window.intent.postResult(this.styleCode)
                setTimeout(() => {
                    let owner = window.opener || window.parent
                    owner.window.close()
                }, 100)
            },
            loadStyle() {
                let url = this.style + '?time=' + new Date().getTime()
                this.$http.get(url).then(
                    response => {
                        let data = response.data
                        console.log(data)
                        this.styleCode = data
                        let style = document.getElementById('style')
                        style.innerHTML = data
                    },
                    response => {
                        console.log(response)
                    })
            }
        },
        watch: {
            style() {
                this.loadStyle()
            }
        }
    }
</script>

<style scoped>
.select {
    margin-bottom: 16px;
}
.article {
    padding: 16px;
}
</style>
