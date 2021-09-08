<template>
    <div class='navigation'>
        <!-- <p>hello world</p> -->
        <el-menu class="el-menu"
                 mode="horizontal"
                 background-color="#5A61A6"
                 text-color="#fff"
                 @select="handleSelect"
                 :router="true"
                 active-text-color="#ffd04b">
            <el-menu-item  index="1" style="font-size: 2vw" class="hide-icon">Western Region Climate Center</el-menu-item>
            <el-menu-item>
                <el-input  @keyup.enter.native="search(search_term)" placeholder="Search for communities or resources..." v-model="search_term">
                    <el-button slot="append" icon="el-icon-search"></el-button>
                </el-input>
            </el-menu-item>
            <!-- <el-menu-item  class="hide-nav-signed"><i class="el-icon-folder-add"  style="color: #FFFFFF"></i>New Community</el-menu-item> -->
            <!-- <el-menu-item  index="1" style="font-size: 2vw" :route="{name:'UDashboard'}" class="hide-icon">WRCC</el-menu-item> -->
        </el-menu>
            
    </div>
</template>

<script>

</script>