<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MC小百科 - 我的世界我的世界玩家社区</title>
    <!-- 外部资源引入 -->
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
    
    <!-- Tailwind 配置 -->
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        mc: {
                            green: '#7CB342', // 我的世界主色调
                            brown: '#8B4513',
                            blue: '#3498DB',
                            accent: '#FFC107'
                        },
                        dark: '#1E293B',
                        light: '#F8FAFC'
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        qfont: ['Comic Sans MS', 'Marker Felt', 'Arial Rounded MT Bold', 'sans-serif'] // Q版字体
                    },
                }
            }
        }
    </script>
    
    <!-- 自定义工具类 -->
    <style type="text/tailwindcss">
        @layer utilities {
            .content-auto {
                content-visibility: auto;
            }
            .hover-lift {
                transition: transform 0.2s ease, box-shadow 0.2s ease;
            }
            .hover-lift:hover {
                transform: translateY(-3px);
                box-shadow: 0 10px 20px rgba(0,0,0,0.1);
            }
            .nav-active {
                border-bottom: 2px solid theme('colors.mc.green');
            }
            .scrollbar-thin {
                scrollbar-width: thin;
            }
            .scrollbar-thin::-webkit-scrollbar {
                width: 4px;
            }
            .scrollbar-thin::-webkit-scrollbar-thumb {
                background-color: rgba(156, 163, 175, 0.5);
                border-radius: 2px;
            }
        }
    </style>
</head>
<body class="bg-gray-50 font-sans text-dark">
    <!-- 顶部导航栏 -->
    <header id="navbar" class="sticky top-0 z-50 bg-white shadow-sm transition-all duration-300">
        <div class="container mx-auto px-4">
            <div class="flex items-center justify-between h-16">
                <!-- Logo区域 -->
                <div class="flex items-center space-x-2">
                    <div class="w-10 h-10 rounded-lg bg-mc-green flex items-center justify-center">
                        <span class="text-white font-bold text-xl">MC</span>
                    </div>
                    <span class="text-xl font-bold bg-gradient-to-r from-mc-green to-mc-blue bg-clip-text text-transparent">MC小百科</span>
                </div>
                
                <!-- 主导航 - 桌面版 -->
                <nav class="hidden md:flex items-center space-x-6">
                    <a href="#" class="nav-active py-5 font-medium text-mc-green">首页</a>
                    <a href="#forum" class="py-5 font-medium hover:text-mc-green transition-colors">论坛</a>
                    <a href="#resources" class="py-5 font-medium hover:text-mc-green transition-colors">资源</a>
                    <a href="#versions" class="py-5 font-medium hover:text-mc-green transition-colors">版本分类</a>
                </nav>
                
                <!-- 功能按钮区 -->
                <div class="flex items-center space-x-3">
                    <button id="searchBtn" class="p-2 rounded-full hover:bg-gray-100 transition-colors">
                        <i class="fa fa-search text-gray-600"></i>
                    </button>
                    
                    <button id="messageBtn" class="p-2 rounded-full hover:bg-gray-100 transition-colors relative">
                        <i class="fa fa-envelope text-gray-600"></i>
                        <span id="messageBadge" class="absolute top-0 right-0 w-4 h-4 bg-red-500 text-white text-xs rounded-full flex items-center justify-center hidden">3</span>
                    </button>
                    
                    <button id="createPostBtn" class="hidden md:flex items-center px-4 py-2 bg-mc-green text-white rounded-full hover:bg-mc-green/90 transition-colors">
                        <i class="fa fa-plus mr-2"></i>发布
                    </button>
                    
                    <!-- 用户菜单 -->
                    <div id="userMenuContainer" class="relative">
                        <button id="userMenuBtn" class="flex items-center justify-center w-10 h-10 rounded-full bg-gray-200 hover:bg-gray-300 transition-colors">
                            <i class="fa fa-user text-gray-600"></i>
                        </button>
                        
                        <!-- 用户下拉菜单 -->
                        <div id="userDropdown" class="absolute right-0 mt-2 w-48 bg-white rounded-lg shadow-lg py-2 hidden z-50">
                            <a href="#" id="loginLink" class="block px-4 py-2 hover:bg-gray-100 transition-colors">
                                <i class="fa fa-sign-in mr-2"></i>登录
                            </a>
                            <a href="#" id="registerLink" class="block px-4 py-2 hover:bg-gray-100 transition-colors">
                                <i class="fa fa-user-plus mr-2"></i>注册
                            </a>
                            <div id="userLoggedInContent" class="hidden">
                                <div class="px-4 py-2 border-t border-gray-100">
                                    <p id="currentUsername" class="text-sm font-medium"></p>
                                </div>
                                <a href="#profile" class="block px-4 py-2 hover:bg-gray-100 transition-colors">
                                    <i class="fa fa-user-circle mr-2"></i>个人中心
                                </a>
                                <a href="#collections" class="block px-4 py-2 hover:bg-gray-100 transition-colors">
                                    <i class="fa fa-bookmark mr-2"></i>我的收藏
                                </a>
                                <a href="#following" class="block px-4 py-2 hover:bg-gray-100 transition-colors">
                                    <i class="fa fa-users mr-2"></i>我的关注
                                </a>
                                <a href="#likes" class="block px-4 py-2 hover:bg-gray-100 transition-colors">
                                    <i class="fa fa-thumbs-up mr-2"></i>我的点赞
                                </a>
                                <a href="#" id="logoutBtn" class="block px-4 py-2 hover:bg-gray-100 transition-colors text-red-500">
                                    <i class="fa fa-sign-out mr-2"></i>退出登录
                                </a>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 移动端菜单按钮 -->
                    <button id="mobileMenuBtn" class="md:hidden p-2 rounded-full hover:bg-gray-100 transition-colors">
                        <i class="fa fa-bars text-gray-600"></i>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- 移动端导航菜单 -->
        <div id="mobileMenu" class="md:hidden bg-white border-t hidden">
            <div class="container mx-auto px-4 py-3 space-y-3">
                <a href="#" class="block py-2 font-medium text-mc-green">首页</a>
                <a href="#forum" class="block py-2 font-medium hover:text-mc-green transition-colors">论坛</a>
                <a href="#resources" class="block py-2 font-medium hover:text-mc-green transition-colors">资源</a>
                <a href="#versions" class="block py-2 font-medium hover:text-mc-green transition-colors">版本分类</a>
                <button class="w-full flex items-center justify-center px-4 py-2 bg-mc-green text-white rounded-full hover:bg-mc-green/90 transition-colors">
                    <i class="fa fa-plus mr-2"></i>发布内容
                </button>
            </div>
        </div>
    </header>

    <main>
        <!-- 头部横幅 -->
        <section class="relative bg-gradient-to-r from-dark to-gray-800 text-white py-16 md:py-24 overflow-hidden">
            <div class="absolute inset-0 opacity-20">
                <img src="https://picsum.photos/id/1048/1920/1080" alt="我的世界背景图" class="w-full h-full object-cover">
            </div>
            <div class="container mx-auto px-4 relative z-10">
                <div class="max-w-3xl">
                    <h1 class="text-[clamp(1.8rem,4vw,3rem)] font-bold mb-4 leading-tight">
                        探索我的世界<br>分享游戏乐趣
                    </h1>
                    <p class="text-lg md:text-xl text-gray-200 mb-8">
                        加入MC小百科社区，与全球玩家一起交流经验、分享资源、探讨技巧
                    </p>
                    <div class="flex flex-wrap gap-4">
                        <a href="#forum" class="px-6 py-3 bg-mc-green text-white rounded-full hover:bg-mc-green/90 transition-colors font-medium">
                            进入论坛
                        </a>
                        <a href="#createPostModal" class="px-6 py-3 bg-white/10 backdrop-blur-sm text-white border border-white/30 rounded-full hover:bg-white/20 transition-colors font-medium">
                            发布内容
                        </a>
                    </div>
                </div>
                
                <!-- 原作者信息 -->
                <div class="mt-12 md:mt-16 flex items-center">
                    <img src="https://picsum.photos/id/237/100/100" alt="小李爱玩电脑的头像" class="w-12 h-12 rounded-full border-2 border-white object-cover">
                    <a href="https://space.bilibili.com/3546822511429785?spm_id_from=333.1007.0.0" target="_blank" class="ml-4 font-qfont text-xl text-red-400 hover:text-red-300 transition-colors cursor-pointer">
                        原作者: 小李爱玩电脑
                    </a>
                </div>
            </div>
        </section>
        
        <!-- 版本分类区域 -->
        <section id="versions" class="py-16 bg-white">
            <div class="container mx-auto px-4">
                <h2 class="text-3xl font-bold mb-2 text-center">选择MC版本</h2>
                <p class="text-gray-600 text-center mb-12 max-w-2xl mx-auto">浏览不同版本的我的世界内容和资源</p>
                
                <!-- 版本大类 -->
                <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-12">
                    <a href="version-java.html" class="hover-lift bg-mc-green/10 border border-mc-green/30 rounded-xl p-6 flex flex-col items-center text-center hover:bg-mc-green/20">
                        <div class="w-16 h-16 rounded-full bg-mc-green flex items-center justify-center mb-4">
                            <i class="fa fa-code text-white text-2xl"></i>
                        </div>
                        <h3 class="font-bold text-lg">Java版</h3>
                    </a>
                    
                    <a href="version-bedrock.html" class="hover-lift bg-mc-blue/10 border border-mc-blue/30 rounded-xl p-6 flex flex-col items-center text-center hover:bg-mc-blue/20">
                        <div class="w-16 h-16 rounded-full bg-mc-blue flex items-center justify-center mb-4">
                            <i class="fa fa-mobile text-white text-2xl"></i>
                        </div>
                        <h3 class="font-bold text-lg">基岩版</h3>
                    </a>
                    
                    <a href="version-netease.html" class="hover-lift bg-red-500/10 border border-red-500/30 rounded-xl p-6 flex flex-col items-center text-center hover:bg-red-500/20">
                        <div class="w-16 h-16 rounded-full bg-red-500 flex items-center justify-center mb-4">
                            <i class="fa fa-rocket text-white text-2xl"></i>
                        </div>
                        <h3 class="font-bold text-lg">网易版</h3>
                    </a>
                    
                    <a href="version-history.html" class="hover-lift bg-mc-brown/10 border border-mc-brown/30 rounded-xl p-6 flex flex-col items-center text-center hover:bg-mc-brown/20">
                        <div class="w-16 h-16 rounded-full bg-mc-brown flex items-center justify-center mb-4">
                            <i class="fa fa-history text-white text-2xl"></i>
                        </div>
                        <h3 class="font-bold text-lg">历史版本</h3>
                    </a>
                </div>
                
                <!-- 历史版本号 -->
                <div>
                    <h3 class="text-xl font-bold mb-6 text-center">历史版本号</h3>
                    <div class="flex flex-wrap justify-center gap-3">
                        <a href="version-1.12.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.12</a>
                        <a href="version-1.13.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.13</a>
                        <a href="version-1.14.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.14</a>
                        <a href="version-1.15.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.15</a>
                        <a href="version-1.16.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.16</a>
                        <a href="version-1.17.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.17</a>
                        <a href="version-1.18.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.18</a>
                        <a href="version-1.19.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.19</a>
                        <a href="version-1.20.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.20</a>
                        <a href="version-1.21.html" class="hover-lift px-4 py-2 bg-gray-100 rounded-full hover:bg-gray-200">1.21</a>
                    </div>
                </div>
            </div>
        </section>
        
        <!-- 论坛内容区 -->
        <section id="forum" class="py-16 bg-gray-50">
            <div class="container mx-auto px-4">
                <div class="flex flex-col md:flex-row gap-8">
                    <!-- 左侧边栏 -->
                    <div class="md:w-1/4 lg:w-1/5">
                        <div class="bg-white rounded-xl shadow-sm p-6 sticky top-20">
                            <h3 class="text-lg font-bold mb-4">论坛分类</h3>
                            <ul class="space-y-2">
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg bg-mc-green/10 text-mc-green">
                                        <i class="fa fa-fire mr-3 w-5 text-center"></i>
                                        <span>热门讨论</span>
                                    </a>
                                </li>
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg hover:bg-gray-100 transition-colors">
                                        <i class="fa fa-newspaper-o mr-3 w-5 text-center"></i>
                                        <span>新闻资讯</span>
                                    </a>
                                </li>
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg hover:bg-gray-100 transition-colors">
                                        <i class="fa fa-lightbulb-o mr-3 w-5 text-center"></i>
                                        <span>教程技巧</span>
                                    </a>
                                </li>
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg hover:bg-gray-100 transition-colors">
                                        <i class="fa fa-picture-o mr-3 w-5 text-center"></i>
                                        <span>作品展示</span>
                                    </a>
                                </li>
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg hover:bg-gray-100 transition-colors">
                                        <i class="fa fa-map mr-3 w-5 text-center"></i>
                                        <span>地图资源</span>
                                    </a>
                                </li>
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg hover:bg-gray-100 transition-colors">
                                        <i class="fa fa-users mr-3 w-5 text-center"></i>
                                        <span>服务器交流</span>
                                    </a>
                                </li>
                                <li>
                                    <a href="#" class="flex items-center p-2 rounded-lg hover:bg-gray-100 transition-colors">
                                        <i class="fa fa-question-circle mr-3 w-5 text-center"></i>
                                        <span>问题求助</span>
                                    </a>
                                </li>
                            </ul>
                            
                            <div class="mt-8 pt-6 border-t border-gray-100">
                                <h3 class="text-lg font-bold mb-4">活跃用户</h3>
                                <div class="space-y-4">
                                    <div class="flex items-center">
                                        <img src="https://picsum.photos/id/1005/100/100" alt="用户头像" class="w-10 h-10 rounded-full">
                                        <div class="ml-3">
                                            <p class="font-medium text-sm">红石大师</p>
                                            <p class="text-xs text-gray-500">发布了32篇内容</p>
                                        </div>
                                        <button class="ml-auto follow-btn px-2 py-1 text-xs border border-mc-green text-mc-green rounded-full hover:bg-mc-green hover:text-white transition-colors">
                                            关注
                                        </button>
                                    </div>
                                    <div class="flex items-center">
                                        <img src="https://picsum.photos/id/1012/100/100" alt="用户头像" class="w-10 h-10 rounded-full">
                                        <div class="ml-3">
                                            <p class="font-medium text-sm">建筑达人</p>
                                            <p class="text-xs text-gray-500">发布了28篇内容</p>
                                        </div>
                                        <button class="ml-auto follow-btn px-2 py-1 text-xs border border-mc-green text-mc-green rounded-full hover:bg-mc-green hover:text-white transition-colors">
                                            关注
                                        </button>
                                    </div>
                                    <div class="flex items-center">
                                        <img src="https://picsum.photos/id/1025/100/100" alt="用户头像" class="w-10 h-10 rounded-full">
                                        <div class="ml-3">
                                            <p class="font-medium text-sm">模组专家</p>
                                            <p class="text-xs text-gray-500">发布了45篇内容</p>
                                        </div>
                                        <button class="ml-auto follow-btn px-2 py-1 text-xs border border-mc-green text-mc-green rounded-full hover:bg-mc-green hover:text-white transition-colors">
                                            关注
                                        </button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 右侧主内容区 -->
                    <div class="md:w-3/4 lg:w-4/5">
                        <!-- 帖子排序和筛选 -->
                        <div class="bg-white rounded-xl shadow-sm p-4 mb-6">
                            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
                                <div class="flex space-x-2">
                                    <button class="px-4 py-2 bg-mc-green text-white rounded-lg text-sm">最新发布</button>
                                    <button class="px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded-lg text-sm transition-colors">热门推荐</button>
                                    <button class="px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded-lg text-sm transition-colors">最多评论</button>
                                </div>
                                
                                <div class="w-full sm:w-auto">
                                    <select class="w-full sm:w-auto px-4 py-2 border border-gray-200 rounded-lg text-sm focus:outline-none focus:ring-2 focus:ring-mc-green/50">
                                        <option value="">所有版本</option>
                                        <option value="java">Java版</option>
                                        <option value="bedrock">基岩版</option>
                                        <option value="netease">网易版</option>
                                        <option value="history">历史版本</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        
                        <!-- 帖子列表 -->
                        <div class="space-y-6">
                            <!-- 帖子1 - 视频类型 -->
                            <article class="bg-white rounded-xl shadow-sm overflow-hidden hover-lift">
                                <div class="p-6">
                                    <div class="flex items-start">
                                        <img src="https://picsum.photos/id/1005/100/100" alt="用户头像" class="w-10 h-10 rounded-full">
                                        <div class="ml-3 flex-1">
                                            <div class="flex items-center">
                                                <h4 class="font-medium">红石大师</h4>
                                                <span class="ml-2 px-2 py-0.5 bg-blue-100 text-blue-800 text-xs rounded-full">Java版</span>
                                                <span class="ml-auto text-sm text-gray-500">2小时前</span>
                                            </div>
                                            <h3 class="mt-2 text-xl font-bold hover:text-mc-green transition-colors">
                                                <a href="post.html">1.21版本全新红石元件教程与应用展示</a>
                                            </h3>
                                            <p class="mt-2 text-gray-600 line-clamp-2">
                                                本视频将详细介绍1.21版本新增的红石元件特性和使用方法，包括如何搭建高效的红石机械和自动化系统...
                                            </p>
                                            
                                            <!-- 视频缩略图 -->
                                            <div class="mt-4 rounded-lg overflow-hidden relative">
                                                <img src="https://picsum.photos/id/1039/800/450" alt="视频缩略图" class="w-full h-48 object-cover">
                                                <div class="absolute inset-0 bg-black/30 flex items-center justify-center">
                                                    <button class="w-14 h-14 rounded-full bg-white/20 backdrop-blur-sm flex items-center justify-center text-white hover:bg-white/30 transition-colors">
                                                        <i class="fa fa-play text-2xl ml-1"></i>
                                                    </button>
                                                </div>
                                                <span class="absolute bottom-2 right-2 bg-black/70 text-white text-xs px-2 py-1 rounded">18:35</span>
                                            </div>
                                            
                                            <div class="mt-4 flex items-center justify-between">
                                                <div class="flex items-center space-x-6">
                                                    <button class="like-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-thumbs-up mr-1"></i>
                                                        <span>128</span>
                                                    </button>
                                                    <button class="comment-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-comment mr-1"></i>
                                                        <span>36</span>
                                                    </button>
                                                    <button class="collect-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-bookmark mr-1"></i>
                                                        <span>42</span>
                                                    </button>
                                                </div>
                                                <button class="share-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                    <i class="fa fa-share mr-1"></i>
                                                    <span>分享</span>
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </article>
                            
                            <!-- 帖子2 - 图片类型 -->
                            <article class="bg-white rounded-xl shadow-sm overflow-hidden hover-lift">
                                <div class="p-6">
                                    <div class="flex items-start">
                                        <img src="https://picsum.photos/id/1012/100/100" alt="用户头像" class="w-10 h-10 rounded-full">
                                        <div class="ml-3 flex-1">
                                            <div class="flex items-center">
                                                <h4 class="font-medium">建筑达人</h4>
                                                <span class="ml-2 px-2 py-0.5 bg-purple-100 text-purple-800 text-xs rounded-full">基岩版</span>
                                                <span class="ml-auto text-sm text-gray-500">昨天 15:30</span>
                                            </div>
                                            <h3 class="mt-2 text-xl font-bold hover:text-mc-green transition-colors">
                                                <a href="post.html">耗时3个月建造的中世纪城堡，细节拉满</a>
                                            </h3>
                                            <p class="mt-2 text-gray-600 line-clamp-2">
                                                这是我在基岩版上建造的中世纪城堡，包含主城堡、护城河、村庄和农场，所有建筑都遵循中世纪风格...
                                            </p>
                                            
                                            <!-- 图片展示 -->
                                            <div class="mt-4 grid grid-cols-3 gap-2 rounded-lg overflow-hidden">
                                                <img src="https://picsum.photos/id/1061/400/300" alt="城堡图片1" class="w-full h-32 object-cover">
                                                <img src="https://picsum.photos/id/1062/400/300" alt="城堡图片2" class="w-full h-32 object-cover">
                                                <img src="https://picsum.photos/id/1063/400/300" alt="城堡图片3" class="w-full h-32 object-cover">
                                            </div>
                                            
                                            <div class="mt-4 flex items-center justify-between">
                                                <div class="flex items-center space-x-6">
                                                    <button class="like-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-thumbs-up mr-1"></i>
                                                        <span>356</span>
                                                    </button>
                                                    <button class="comment-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-comment mr-1"></i>
                                                        <span>89</span>
                                                    </button>
                                                    <button class="collect-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-bookmark mr-1"></i>
                                                        <span>124</span>
                                                    </button>
                                                </div>
                                                <button class="share-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                    <i class="fa fa-share mr-1"></i>
                                                    <span>分享</span>
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </article>
                            
                            <!-- 帖子3 - 文字类型 -->
                            <article class="bg-white rounded-xl shadow-sm overflow-hidden hover-lift">
                                <div class="p-6">
                                    <div class="flex items-start">
                                        <img src="https://picsum.photos/id/1025/100/100" alt="用户头像" class="w-10 h-10 rounded-full">
                                        <div class="ml-3 flex-1">
                                            <div class="flex items-center">
                                                <h4 class="font-medium">模组专家</h4>
                                                <span class="ml-2 px-2 py-0.5 bg-yellow-100 text-yellow-800 text-xs rounded-full">1.20</span>
                                                <span class="ml-auto text-sm text-gray-500">3天前</span>
                                            </div>
                                            <h3 class="mt-2 text-xl font-bold hover:text-mc-green transition-colors">
                                                <a href="post.html">1.20版本必装的10个实用模组推荐</a>
                                            </h3>
                                            <p class="mt-2 text-gray-600 line-clamp-3">
                                                今天给大家推荐10个1.20版本非常实用的模组，涵盖了建筑、生存、红石和冒险等多个方面，每个模组都能极大提升游戏体验...
                                                <br><br>
                                                1. Xaero的地图模组 - 提供了详细的地图和小地图功能，支持Waypoint标记...
                                                2. 更好的村民模组 - 改进了村民的AI和交易系统...
                                            </p>
                                            
                                            <div class="mt-4 flex items-center justify-between">
                                                <div class="flex items-center space-x-6">
                                                    <button class="like-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-thumbs-up mr-1"></i>
                                                        <span>215</span>
                                                    </button>
                                                    <button class="comment-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-comment mr-1"></i>
                                                        <span>67</span>
                                                    </button>
                                                    <button class="collect-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                        <i class="fa fa-bookmark mr-1"></i>
                                                        <span>93</span>
                                                    </button>
                                                </div>
                                                <button class="share-btn flex items-center text-gray-500 hover:text-mc-green transition-colors">
                                                    <i class="fa fa-share mr-1"></i>
                                                    <span>分享</span>
                                                </button>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </article>
                        </div>
                        
                        <!-- 加载更多 -->
                        <div class="mt-8 text-center">
                            <button id="loadMoreBtn" class="px-6 py-3 border border-gray-300 rounded-full hover:bg-gray-50 transition-colors">
                                加载更多内容 <i class="fa fa-refresh ml-1"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- 页脚 -->
    <footer class="bg-dark text-white pt-16 pb-8 mt-16">
        <div class="container mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-8 mb-12">
                <div>
                    <div class="flex items-center space-x-2 mb-6">
                        <div class="w-10 h-10 rounded-lg bg-mc-green flex items-center justify-center">
                            <span class="text-white font-bold text-xl">MC</span>
                        </div>
                        <span class="text-xl font-bold">MC小百科</span>
                    </div>
                    <p class="text-gray-400 mb-6">
                        专注于我的世界游戏的玩家社区，分享经验、交流技巧、发布资源
                    </p>
                    <div class="flex space-x-4">
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-mc-green transition-colors">
                            <i class="fa fa-bilibili"></i>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-mc-green transition-colors">
                            <i class="fa fa-weixin"></i>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-mc-green transition-colors">
                            <i class="fa fa-weibo"></i>
                        </a>
                        <a href="#" class="w-10 h-10 rounded-full bg-gray-800 flex items-center justify-center hover:bg-mc-green transition-colors">
                            <i class="fa fa-youtube-play"></i>
                        </a>
                    </div>
                </div>
                
                <div>
                    <h3 class="text-lg font-bold mb-6">快速链接</h3>
                    <ul class="space-y-3">
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">首页</a></li>
                        <li><a href="#forum" class="text-gray-400 hover:text-white transition-colors">论坛</a></li>
                        <li><a href="#resources" class="text-gray-400 hover:text-white transition-colors">资源</a></li>
                        <li><a href="#versions" class="text-gray-400 hover:text-white transition-colors">版本分类</a></li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="text-lg font-bold mb-6">支持</h3>
                    <ul class="space-y-3">
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">帮助中心</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">社区规范</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">反馈建议</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">联系我们</a></li>
                    </ul>
                </div>
                
                <div>
                    <h3 class="text-lg font-bold mb-6">关于</h3>
                    <ul class="space-y-3">
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">平台介绍</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">加入我们</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">隐私政策</a></li>
                        <li><a href="#" class="text-gray-400 hover:text-white transition-colors">用户协议</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-gray-800 pt-8 text-center text-gray-500 text-sm">
                <p>© 2025 MC小百科 版权所有 | 原作者: <a href="https://space.bilibili.com/3546822511429785?spm_id_from=333.1007.0.0" target="_blank" class="font-qfont text-red-400 hover:underline">小李爱玩电脑</a></p>
            </div>
        </div>
    </footer>

    <!-- 登录模态框 -->
    <div id="loginModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm hidden">
        <div class="bg-white rounded-xl shadow-2xl w-full max-w-md p-6 md:p-8 transform transition-all animate-fadeIn">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-2xl font-bold">登录</h3>
                <button id="closeLoginModal" class="text-gray-500 hover:text-gray-700">
                    <i class="fa fa-times text-xl"></i>
                </button>
            </div>
            
            <form id="loginForm">
                <div class="mb-4">
                    <label for="loginUsername" class="block text-sm font-medium text-gray-700 mb-1">用户名</label>
                    <input type="text" id="loginUsername" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请输入用户名" required>
                </div>
                
                <div class="mb-6">
                    <label for="loginPassword" class="block text-sm font-medium text-gray-700 mb-1">密码</label>
                    <input type="password" id="loginPassword" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请输入密码" required>
                    <div class="flex justify-end mt-1">
                        <a href="#" class="text-sm text-mc-green hover:underline">忘记密码？</a>
                    </div>
                </div>
                
                <button type="submit" class="w-full py-3 bg-mc-green text-white rounded-lg font-medium hover:bg-mc-green/90 transition-colors mb-4">
                    登录
                </button>
                
                <p class="text-center text-gray-600">
                    还没有账号？ <a href="#" id="switchToRegister" class="text-mc-green hover:underline">立即注册</a>
                </p>
            </form>
        </div>
    </div>
    
    <!-- 注册模态框 -->
    <div id="registerModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm hidden">
        <div class="bg-white rounded-xl shadow-2xl w-full max-w-md p-6 md:p-8 transform transition-all animate-fadeIn">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-2xl font-bold">注册</h3>
                <button id="closeRegisterModal" class="text-gray-500 hover:text-gray-700">
                    <i class="fa fa-times text-xl"></i>
                </button>
            </div>
            
            <form id="registerForm">
                <div class="mb-4">
                    <label for="registerUsername" class="block text-sm font-medium text-gray-700 mb-1">用户名</label>
                    <input type="text" id="registerUsername" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请设置用户名" required>
                    <p id="usernameError" class="text-red-500 text-xs mt-1 hidden">用户名已存在</p>
                </div>
                
                <div class="mb-4">
                    <label for="registerEmail" class="block text-sm font-medium text-gray-700 mb-1">邮箱</label>
                    <input type="email" id="registerEmail" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请输入邮箱" required>
                </div>
                
                <div class="mb-4">
                    <label for="registerPassword" class="block text-sm font-medium text-gray-700 mb-1">密码</label>
                    <input type="password" id="registerPassword" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请设置密码（至少8位，包含字母和数字）" required>
                    <p id="passwordError" class="text-red-500 text-xs mt-1 hidden">密码不符合要求（至少8位，包含字母和数字，无特殊符号）</p>
                </div>
                
                <div class="mb-6">
                    <label for="registerConfirmPassword" class="block text-sm font-medium text-gray-700 mb-1">确认密码</label>
                    <input type="password" id="registerConfirmPassword" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请再次输入密码" required>
                    <p id="confirmError" class="text-red-500 text-xs mt-1 hidden">两次输入的密码不一致</p>
                </div>
                
                <button type="submit" class="w-full py-3 bg-mc-green text-white rounded-lg font-medium hover:bg-mc-green/90 transition-colors mb-4">
                    注册
                </button>
                
                <p class="text-center text-gray-600">
                    已有账号？ <a href="#" id="switchToLogin" class="text-mc-green hover:underline">立即登录</a>
                </p>
            </form>
        </div>
    </div>
    
    <!-- 发布内容模态框 -->
    <div id="createPostModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm hidden">
        <div class="bg-white rounded-xl shadow-2xl w-full max-w-3xl max-h-[90vh] overflow-y-auto transform transition-all animate-fadeIn">
            <div class="p-6 md:p-8">
                <div class="flex justify-between items-center mb-6">
                    <h3 class="text-2xl font-bold">发布内容</h3>
                    <button id="closeCreatePostModal" class="text-gray-500 hover:text-gray-700">
                        <i class="fa fa-times text-xl"></i>
                    </button>
                </div>
                
                <form id="createPostForm">
                    <!-- 内容类型选择 -->
                    <div class="mb-6">
                        <label class="block text-sm font-medium text-gray-700 mb-3">内容类型</label>
                        <div class="flex flex-wrap gap-3">
                            <button type="button" class="content-type-btn px-4 py-2 bg-mc-green text-white rounded-lg flex items-center">
                                <i class="fa fa-file-text-o mr-2"></i>文字帖
                            </button>
                            <button type="button" class="content-type-btn px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded-lg flex items-center transition-colors">
                                <i class="fa fa-picture-o mr-2"></i>图片帖
                            </button>
                            <button type="button" class="content-type-btn px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded-lg flex items-center transition-colors">
                                <i class="fa fa-video-camera mr-2"></i>视频帖
                            </button>
                        </div>
                    </div>
                    
                    <!-- 帖子标题 -->
                    <div class="mb-4">
                        <label for="postTitle" class="block text-sm font-medium text-gray-700 mb-1">标题</label>
                        <input type="text" id="postTitle" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请输入标题" required>
                    </div>
                    
                    <!-- 版本选择 -->
                    <div class="mb-4">
                        <label for="postVersion" class="block text-sm font-medium text-gray-700 mb-1">MC版本</label>
                        <select id="postVersion" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" required>
                            <option value="">请选择版本</option>
                            <option value="java">Java版</option>
                            <option value="bedrock">基岩版</option>
                            <option value="netease">网易版</option>
                            <option value="1.12">1.12</option>
                            <option value="1.13">1.13</option>
                            <option value="1.14">1.14</option>
                            <option value="1.15">1.15</option>
                            <option value="1.16">1.16</option>
                            <option value="1.17">1.17</option>
                            <option value="1.18">1.18</option>
                            <option value="1.19">1.19</option>
                            <option value="1.20">1.20</option>
                            <option value="1.21">1.21</option>
                        </select>
                    </div>
                    
                    <!-- 内容编辑器 -->
                    <div class="mb-4">
                        <label for="postContent" class="block text-sm font-medium text-gray-700 mb-1">内容</label>
                        <textarea id="postContent" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50 resize-none" rows="6" placeholder="请输入内容... 可以使用@提及其他用户"></textarea>
                        
                        <!-- 编辑器工具栏 -->
                        <div class="flex items-center mt-2 space-x-2 text-gray-600">
                            <button type="button" class="p-1.5 hover:bg-gray-100 rounded" title="粗体">
                                <i class="fa fa-bold"></i>
                            </button>
                            <button type="button" class="p-1.5 hover:bg-gray-100 rounded" title="斜体">
                                <i class="fa fa-italic"></i>
                            </button>
                            <button type="button" class="p-1.5 hover:bg-gray-100 rounded" title="链接">
                                <i class="fa fa-link"></i>
                            </button>
                            <button type="button" class="p-1.5 hover:bg-gray-100 rounded" title="图片">
                                <i class="fa fa-image"></i>
                            </button>
                            <button type="button" class="p-1.5 hover:bg-gray-100 rounded" title="提及用户">
                                <i class="fa fa-at"></i>
                            </button>
                        </div>
                    </div>
                    
                    <!-- 图片/视频上传区域 -->
                    <div id="mediaUploadArea" class="mb-6 hidden">
                        <label class="block text-sm font-medium text-gray-700 mb-3">上传文件</label>
                        <div class="border-2 border-dashed border-gray-300 rounded-lg p-6 text-center hover:border-mc-green transition-colors">
                            <i class="fa fa-cloud-upload text-4xl text-gray-400 mb-3"></i>
                            <p class="text-gray-600 mb-2">点击或拖拽文件到此处上传</p>
                            <p class="text-xs text-gray-500">支持 JPG、PNG、MP4 格式，单个文件不超过 2GB</p>
                            <input type="file" id="mediaFile" accept="image/*,video/*" class="hidden" multiple>
                            <button type="button" id="browseMediaFile" class="mt-4 px-4 py-2 bg-gray-100 text-gray-700 rounded-lg hover:bg-gray-200 transition-colors">
                                选择文件
                            </button>
                        </div>
                        
                        <!-- 已上传文件预览 -->
                        <div id="uploadedFiles" class="mt-4 grid grid-cols-4 gap-2 hidden">
                            <!-- 上传的文件预览会在这里显示 -->
                        </div>
                    </div>
                    
                    <!-- 标签 -->
                    <div class="mb-6">
                        <label for="postTags" class="block text-sm font-medium text-gray-700 mb-1">标签</label>
                        <input type="text" id="postTags" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="请输入标签，用逗号分隔（最多5个）">
                    </div>
                    
                    <div class="flex justify-end space-x-3">
                        <button type="button" id="cancelPost" class="px-6 py-2 border border-gray-300 rounded-lg hover:bg-gray-50 transition-colors">
                            取消
                        </button>
                        <button type="submit" class="px-6 py-2 bg-mc-green text-white rounded-lg hover:bg-mc-green/90 transition-colors">
                            发布
                        </button>
                    </div>
                </form>
            </div>
        </div>
    </div>
    
    <!-- 私信模态框 -->
    <div id="messagesModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50 backdrop-blur-sm hidden">
        <div class="bg-white rounded-xl shadow-2xl w-full max-w-4xl max-h-[90vh] overflow-hidden transform transition-all animate-fadeIn">
            <div class="flex h-full flex-col md:flex-row">
                <!-- 联系人列表 -->
                <div class="w-full md:w-1/3 border-b md:border-b-0 md:border-r border-gray-200 h-64 md:h-full overflow-y-auto scrollbar-thin">
                    <div class="p-4 border-b border-gray-200">
                        <h3 class="font-bold text-lg">私信</h3>
                    </div>
                    
                    <div class="p-3 border-b border-gray-100 bg-blue-50">
                        <div class="flex items-center">
                            <img src="https://picsum.photos/id/1005/100/100" alt="联系人头像" class="w-10 h-10 rounded-full">
                            <div class="ml-3 flex-1">
                                <div class="flex justify-between">
                                    <h4 class="font-medium">红石大师</h4>
                                    <span class="text-xs text-gray-500">10:23</span>
                                </div>
                                <p class="text-sm text-gray-600 truncate">你好，关于你发布的红石教程...</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="p-3 border-b border-gray-100 hover:bg-gray-50 transition-colors">
                        <div class="flex items-center">
                            <img src="https://picsum.photos/id/1012/100/100" alt="联系人头像" class="w-10 h-10 rounded-full">
                            <div class="ml-3 flex-1">
                                <div class="flex justify-between">
                                    <h4 class="font-medium">建筑达人</h4>
                                    <span class="text-xs text-gray-500">昨天</span>
                                </div>
                                <p class="text-sm text-gray-600 truncate">你的城堡建造得真不错！</p>
                            </div>
                        </div>
                    </div>
                    
                    <div class="p-3 border-b border-gray-100 hover:bg-gray-50 transition-colors">
                        <div class="flex items-center">
                            <img src="https://picsum.photos/id/1025/100/100" alt="联系人头像" class="w-10 h-10 rounded-full">
                            <div class="ml-3 flex-1">
                                <div class="flex justify-between">
                                    <h4 class="font-medium">模组专家</h4>
                                    <span class="text-xs text-gray-500">3天前</span>
                                </div>
                                <p class="text-sm text-gray-600 truncate">你推荐的模组很好用，谢谢！</p>
                            </div>
                        </div>
                    </div>
                </div>
                
                <!-- 聊天内容 -->
                <div class="w-full md:w-2/3 h-full flex flex-col">
                    <!-- 聊天头部 -->
                    <div class="p-4 border-b border-gray-200 flex items-center">
                        <img src="https://picsum.photos/id/1005/100/100" alt="聊天对象头像" class="w-10 h-10 rounded-full">
                        <div class="ml-3">
                            <h4 class="font-medium">红石大师</h4>
                            <p class="text-xs text-gray-500">在线</p>
                        </div>
                        <button class="ml-auto text-gray-500 hover:text-gray-700">
                            <i class="fa fa-ellipsis-v"></i>
                        </button>
                    </div>
                    
                    <!-- 聊天消息区 -->
                    <div class="flex-1 p-4 overflow-y-auto scrollbar-thin space-y-4">
                        <div class="flex items-end">
                            <img src="https://picsum.photos/id/1005/100/100" alt="对方头像" class="w-8 h-8 rounded-full">
                            <div class="ml-2 max-w-[80%]">
                                <div class="bg-gray-100 p-3 rounded-lg rounded-tl-none">
                                    <p>你好，关于你发布的红石教程，我有个问题想请教</p>
                                </div>
                                <p class="text-xs text-gray-500 mt-1 ml-2">09:45</p>
                            </div>
                        </div>
                        
                        <div class="flex items-end justify-end">
                            <div class="mr-2 max-w-[80%]">
                                <div class="bg-mc-green text-white p-3 rounded-lg rounded-tr-none">
                                    <p>你好！有什么问题尽管问，我会尽力解答</p>
                                </div>
                                <p class="text-xs text-gray-500 mt-1 mr-2 text-right">10:12</p>
                            </div>
                            <img src="https://picsum.photos/id/237/100/100" alt="我的头像" class="w-8 h-8 rounded-full">
                        </div>
                        
                        <div class="flex items-end">
                            <img src="https://picsum.photos/id/1005/100/100" alt="对方头像" class="w-8 h-8 rounded-full">
                            <div class="ml-2 max-w-[80%]">
                                <div class="bg-gray-100 p-3 rounded-lg rounded-tl-none">
                                    <p>就是关于那个脉冲发生器，我按照教程做了但总是不稳定，不知道是什么原因</p>
                                </div>
                                <p class="text-xs text-gray-500 mt-1 ml-2">10:23</p>
                            </div>
                        </div>
                    </div>
                    
                    <!-- 消息输入区 -->
                    <div class="p-4 border-t border-gray-200">
                        <div class="flex items-center mb-2">
                            <button class="p-2 text-gray-500 hover:text-mc-green transition-colors">
                                <i class="fa fa-smile-o"></i>
                            </button>
                            <button class="p-2 text-gray-500 hover:text-mc-green transition-colors">
                                <i class="fa fa-image"></i>
                            </button>
                            <button class="p-2 text-gray-500 hover:text-mc-green transition-colors">
                                <i class="fa fa-file-o"></i>
                            </button>
                        </div>
                        <div class="flex">
                            <input type="text" id="messageInput" class="flex-1 px-4 py-2 border border-gray-300 rounded-l-lg focus:outline-none focus:ring-2 focus:ring-mc-green/50" placeholder="输入消息...">
                            <button id="sendMessageBtn" class="px-4 py-2 bg-mc-green text-white rounded-r-lg hover:bg-mc-green/90 transition-colors">
                                <i class="fa fa-paper-plane"></i>
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- JavaScript -->
    <script>
        // 模拟数据库
        const mockDB = {
            users: [
                { id: 1, username: 'admin', password: 'Admin1234', email: 'admin@example.com' },
                { id: 2, username: '红石大师', password: 'Redstone123', email: 'redstone@example.com' },
                { id: 3, username: '建筑达人', password: 'Build4567', email: 'build@example.com' }
            ],
            posts: [
                // 帖子数据在HTML中静态展示
            ],
            currentUser: null,
            messages: [
                // 消息数据在HTML中静态展示
            ]
        };
        
        // DOM元素
        const navbar = document.getElementById('navbar');
        const mobileMenuBtn = document.getElementById('mobileMenuBtn');
        const mobileMenu = document.getElementById('mobileMenu');
        const userMenuBtn = document.getElementById('userMenuBtn');
        const userDropdown = document.getElementById('userDropdown');
        const loginLink = document.getElementById('loginLink');
        const registerLink = document.getElementById('registerLink');
        const logoutBtn = document.getElementById('logoutBtn');
        const currentUsername = document.getElementById('currentUsername');
        const userLoggedInContent = document.getElementById('userLoggedInContent');
        const createPostBtn = document.getElementById('createPostBtn');
        const messageBtn = document.getElementById('messageBtn');
        const messageBadge = document.getElementById('messageBadge');
        const loadMoreBtn = document.getElementById('loadMoreBtn');
        
        // 模态框元素
        const loginModal = document.getElementById('loginModal');
        const registerModal = document.getElementById('registerModal');
        const createPostModal = document.getElementById('createPostModal');
        const messagesModal = document.getElementById('messagesModal');
        const closeLoginModal = document.getElementById('closeLoginModal');
        const closeRegisterModal = document.getElementById('closeRegisterModal');
        const closeCreatePostModal = document.getElementById('closeCreatePostModal');
        const switchToRegister = document.getElementById('switchToRegister');
        const switchToLogin = document.getElementById('switchToLogin');
        const cancelPost = document.getElementById('cancelPost');
        
        // 表单元素
        const loginForm = document.getElementById('loginForm');
        const registerForm = document.getElementById('registerForm');
        const createPostForm = document.getElementById('createPostForm');
        const contentTypes = document.querySelectorAll('.content-type-btn');
        const mediaUploadArea = document.getElementById('mediaUploadArea');
        const browseMediaFile = document.getElementById('browseMediaFile');
        const mediaFile = document.getElementById('mediaFile');
        const uploadedFiles = document.getElementById('uploadedFiles');
        const messageInput = document.getElementById('messageInput');
        const sendMessageBtn = document.getElementById('sendMessageBtn');
        
        // 注册表单验证元素
        const registerUsername = document.getElementById('registerUsername');
        const registerPassword = document.getElementById('registerPassword');
        const registerConfirmPassword = document.getElementById('registerConfirmPassword');
        const usernameError = document.getElementById('usernameError');
        const passwordError = document.getElementById('passwordError');
        const confirmError = document.getElementById('confirmError');
        
        // 事件监听 - 导航栏滚动效果
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                navbar.classList.add('shadow-md');
            } else {
                navbar.classList.remove('shadow-md');
            }
        });
        
        // 事件监听 - 移动端菜单
        mobileMenuBtn.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });
        
        // 事件监听 - 用户菜单
        userMenuBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            userDropdown.classList.toggle('hidden');
        });
        
        // 点击其他区域关闭下拉菜单
        document.addEventListener('click', () => {
            userDropdown.classList.add('hidden');
        });
        
        // 阻止下拉菜单内部点击事件冒泡
        userDropdown.addEventListener('click', (e) => {
            e.stopPropagation();
        });
        
        // 事件监听 - 模态框控制
        loginLink.addEventListener('click', (e) => {
            e.preventDefault();
            loginModal.classList.remove('hidden');
            registerModal.classList.add('hidden');
            userDropdown.classList.add('hidden');
        });
        
        registerLink.addEventListener('click', (e) => {
            e.preventDefault();
            registerModal.classList.remove('hidden');
            loginModal.classList.add('hidden');
            userDropdown.classList.add('hidden');
        });
        
        createPostBtn.addEventListener('click', (e) => {
            e.preventDefault();
            // 检查是否登录
            if (mockDB.currentUser) {
                createPostModal.classList.remove('hidden');
            } else {
                loginModal.classList.remove('hidden');
                alert('请先登录后再发布内容');
            }
        });
        
        messageBtn.addEventListener('click', () => {
            // 检查是否登录
            if (mockDB.currentUser) {
                messagesModal.classList.remove('hidden');
            } else {
                loginModal.classList.remove('hidden');
                alert('请先登录后再查看消息');
            }
        });
        
        closeLoginModal.addEventListener('click', () => {
            loginModal.classList.add('hidden');
        });
        
        closeRegisterModal.addEventListener('click', () => {
            registerModal.classList.add('hidden');
        });
        
        closeCreatePostModal.addEventListener('click', () => {
            createPostModal.classList.add('hidden');
        });
        
        switchToRegister.addEventListener('click', (e) => {
            e.preventDefault();
            loginModal.classList.add('hidden');
            registerModal.classList.remove('hidden');
        });
        
        switchToLogin.addEventListener('click', (e) => {
            e.preventDefault();
            registerModal.classList.add('hidden');
            loginModal.classList.remove('hidden');
        });
        
        cancelPost.addEventListener('click', () => {
            createPostModal.classList.add('hidden');
        });
        
        // 内容类型选择
        contentTypes.forEach(btn => {
            btn.addEventListener('click', () => {
                // 重置所有按钮样式
                contentTypes.forEach(b => {
                    b.classList.remove('bg-mc-green', 'text-white');
                    b.classList.add('bg-gray-100', 'hover:bg-gray-200');
                });
                
                // 设置当前按钮样式
                btn.classList.remove('bg-gray-100', 'hover:bg-gray-200');
                btn.classList.add('bg-mc-green', 'text-white');
                
                // 显示/隐藏媒体上传区域
                if (btn.textContent.includes('图片') || btn.textContent.includes('视频')) {
                    mediaUploadArea.classList.remove('hidden');
                } else {
                    mediaUploadArea.classList.add('hidden');
                }
            });
        });
        
        // 媒体文件选择
        browseMediaFile.addEventListener('click', () => {
            mediaFile.click();
        });
        
        mediaFile.addEventListener('change', (e) => {
            if (e.target.files.length > 0) {
                uploadedFiles.classList.remove('hidden');
                uploadedFiles.innerHTML = '';
                
                // 显示已选择的文件预览
                for (let i = 0; i < e.target.files.length; i++) {
                    const file = e.target.files[i];
                    const filePreview = document.createElement('div');
                    filePreview.className = 'relative rounded overflow-hidden';
                    
                    if (file.type.startsWith('image/')) {
                        // 图片预览
                        const reader = new FileReader();
                        reader.onload = function(event) {
                            filePreview.innerHTML = `
                                <img src="${event.target.result}" alt="预览图" class="w-full h-20 object-cover">
                                <button class="absolute top-1 right-1 w-5 h-5 bg-black/50 text-white rounded-full flex items-center justify-center hover:bg-black/70 transition-colors">
                                    <i class="fa fa-times text-xs"></i>
                                </button>
                            `;
                            uploadedFiles.appendChild(filePreview);
                        };
                        reader.readAsDataURL(file);
                    } else if (file.type.startsWith('video/')) {
                        // 视频预览
                        filePreview.innerHTML = `
                            <div class="w-full h-20 bg-gray-100 flex items-center justify-center">
                                <i class="fa fa-video-camera text-gray-400 text-2xl"></i>
                            </div>
                            <button class="absolute top-1 right-1 w-5 h-5 bg-black/50 text-white rounded-full flex items-center justify-center hover:bg-black/70 transition-colors">
                                <i class="fa fa-times text-xs"></i>
                            </button>
                        `;
                        uploadedFiles.appendChild(filePreview);
                    }
                }
                
                // 添加删除文件事件
                const deleteButtons = uploadedFiles.querySelectorAll('button');
                deleteButtons.forEach(btn => {
                    btn.addEventListener('click', function() {
                        this.parentElement.remove();
                        if (uploadedFiles.children.length === 0) {
                            uploadedFiles.classList.add('hidden');
                        }
                    });
                });
            }
        });
        
        // 发送消息
        sendMessageBtn.addEventListener('click', () => {
            const messageText = messageInput.value.trim();
            if (messageText) {
                // 在实际应用中，这里会发送消息到服务器
                alert(`消息已发送: ${messageText}`);
                messageInput.value = '';
            }
        });
        
        messageInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                sendMessageBtn.click();
            }
        });
        
        // 登录表单提交
        loginForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('loginUsername').value;
            const password = document.getElementById('loginPassword').value;
            
            // 查找用户
            const user = mockDB.users.find(u => u.username === username && u.password === password);
            
            if (user) {
                mockDB.currentUser = user;
                updateUserInterface();
                loginModal.classList.add('hidden');
                alert('登录成功！');
            } else {
                alert('用户名或密码错误');
            }
        });
        
        // 注册表单验证
        registerUsername.addEventListener('blur', () => {
            const username = registerUsername.value;
            const userExists = mockDB.users.some(u => u.username === username);
            
            if (userExists) {
                usernameError.classList.remove('hidden');
            } else {
                usernameError.classList.add('hidden');
            }
        });
        
        registerPassword.addEventListener('blur', validatePassword);
        
        function validatePassword() {
            const password = registerPassword.value;
            // 密码验证规则：至少8位，包含字母和数字，不包含特殊符号
            const passwordRegex = /^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$/;
            
            if (!passwordRegex.test(password)) {
                passwordError.classList.remove('hidden');
                return false;
            } else {
                passwordError.classList.add('hidden');
                return true;
            }
        }
        
        registerConfirmPassword.addEventListener('blur', () => {
            if (registerConfirmPassword.value !== registerPassword.value) {
                confirmError.classList.remove('hidden');
            } else {
                confirmError.classList.remove('hidden');
            }
        });
        
        // 注册表单提交
        registerForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = registerUsername.value;
            const email = document.getElementById('registerEmail').value;
            const password = registerPassword.value;
            const confirmPassword = registerConfirmPassword.value;
            
            // 验证
            let isValid = true;
            const userExists = mockDB.users.some(u => u.username === username);
            
            if (userExists) {
                usernameError.classList.remove('hidden');
                isValid = false;
            }
            
            if (!validatePassword()) {
                isValid = false;
            }
            
            if (password !== confirmPassword) {
                confirmError.classList.remove('hidden');
                isValid = false;
            }
            
            if (isValid) {
                // 创建新用户
                const newUser = {
                    id: mockDB.users.length + 1,
                    username,
                    password,
                    email
                };
                
                mockDB.users.push(newUser);
                mockDB.currentUser = newUser;
                updateUserInterface();
                registerModal.classList.add('hidden');
                alert('注册成功！');
                
                // 重置表单
                registerForm.reset();
                usernameError.classList.add('hidden');
                passwordError.classList.add('hidden');
                confirmError.classList.add('hidden');
            }
        });
        
        // 发布内容表单提交
        createPostForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const title = document.getElementById('postTitle').value;
            const version = document.getElementById('postVersion').value;
            const content = document.getElementById('postContent').value;
            
            if (!title || !version) {
                alert('请填写标题和选择MC版本');
                return;
            }
            
            alert('内容发布成功！');
            createPostModal.classList.add('hidden');
            createPostForm.reset();
            uploadedFiles.classList.add('hidden');
            uploadedFiles.innerHTML = '';
        });
        
        // 退出登录
        logoutBtn.addEventListener('click', (e) => {
            e.preventDefault();
            mockDB.currentUser = null;
            updateUserInterface();
            userDropdown.classList.add('hidden');
            alert('已退出登录');
        });
        
        // 加载更多内容
        loadMoreBtn.addEventListener('click', () => {
            // 模拟加载中状态
            loadMoreBtn.innerHTML = '<i class="fa fa-spinner fa-spin mr-1"></i> 加载中...';
            
            // 模拟网络请求延迟
            setTimeout(() => {
                loadMoreBtn.innerHTML = '加载更多内容 <i class="fa fa-refresh ml-1"></i>';
                alert('已加载全部内容');
            }, 1500);
        });
        
        // 点赞功能
        document.querySelectorAll('.like-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                if (!mockDB.currentUser) {
                    loginModal.classList.remove('hidden');
                    alert('请先登录后再点赞');
                    return;
                }
                
                const icon = this.querySelector('i');
                const count = this.querySelector('span');
                
                if (icon.classList.contains('text-mc-green')) {
                    // 取消点赞
                    icon.classList.remove('text-mc-green');
                    count.textContent = parseInt(count.textContent) - 1;
                } else {
                    // 点赞
                    icon.classList.add('text-mc-green');
                    count.textContent = parseInt(count.textContent) + 1;
                }
            });
        });
        
        // 收藏功能
        document.querySelectorAll('.collect-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                if (!mockDB.currentUser) {
                    loginModal.classList.remove('hidden');
                    alert('请先登录后再收藏');
                    return;
                }
                
                const icon = this.querySelector('i');
                const text = this.querySelector('span');
                
                if (icon.classList.contains('text-mc-green')) {
                    // 取消收藏
                    icon.classList.remove('text-mc-green');
                    text.textContent = '收藏';
                    alert('已取消收藏');
                } else {
                    // 收藏
                    icon.classList.add('text-mc-green');
                    text.textContent = '已收藏';
                    alert('收藏成功');
                }
            });
        });
        
        // 关注功能
        document.querySelectorAll('.follow-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                if (!mockDB.currentUser) {
                    loginModal.classList.remove('hidden');
                    alert('请先登录后再关注');
                    return;
                }
                
                if (this.textContent.trim() === '关注') {
                    this.textContent = '已关注';
                    this.classList.remove('border-mc-green', 'text-mc-green');
                    this.classList.add('bg-mc-green/10', 'text-gray-600', 'border-gray-200');
                    alert('关注成功');
                } else {
                    this.textContent = '关注';
                    this.classList.add('border-mc-green', 'text-mc-green');
                    this.classList.remove('bg-mc-green/10', 'text-gray-600', 'border-gray-200');
                    alert('已取消关注');
                }
            });
        });
        
        // 更新用户界面
        function updateUserInterface() {
            if (mockDB.currentUser) {
                // 已登录状态
                loginLink.classList.add('hidden');
                registerLink.classList.add('hidden');
                userLoggedInContent.classList.remove('hidden');
                currentUsername.textContent = mockDB.currentUser.username;
                
                // 显示消息徽章
                messageBadge.classList.remove('hidden');
            } else {
                // 未登录状态
                loginLink.classList.remove('hidden');
                registerLink.classList.remove('hidden');
                userLoggedInContent.classList.add('hidden');
                
                // 隐藏消息徽章
                messageBadge.classList.add('hidden');
            }
        }
        
        // 初始化页面
        function init() {
            updateUserInterface();
            
            // 点击外部关闭模态框
            window.addEventListener('click', (e) => {
                if (e.target === loginModal) loginModal.classList.add('hidden');
                if (e.target === registerModal) registerModal.classList.add('hidden');
                if (e.target === createPostModal) createPostModal.classList.add('hidden');
                if (e.target === messagesModal) messagesModal.classList.add('hidden');
            });
            
            // 版本页面跳转逻辑
            document.querySelectorAll('[href^="version-"]').forEach(link => {
                link.addEventListener('click', (e) => {
                    const version = link.getAttribute('href').replace('version-', '').replace('.html', '');
                    e.preventDefault();
                    alert(`即将跳转到 ${version} 版本的页面`);
                });
            });
        }
        
        // 页面加载完成后初始化
        document.addEventListener('DOMContentLoaded', init);
    </script>
</body>
</html>
    
