## Permission Management Methods
### Based on Role
每个用户只能有一个角色，角色之间可以有继承关系。

![permissionModel1](https://raw.github.com/pi-asset/image/master/permission/permissionModel1.jpg)
### Based on Group(in use)
一个用户可以属于多个组，组之间没有关系。

![permissionModel2](https://raw.github.com/pi-asset/image/master/permission/permissionModel2.jpg)
### Combine of Role and Group
资源组合成组，组之间没有关系。一个或多个组构成一个角色，角色之间可以存在继承关系。每个用户有且只有一个角色，同时可以直接把用户加入组，使用户具有该组规定的权限。

采用这种方式避免了使用角色管理权限时需要单独赋予某用户某项权限时的不便，如果使用角色管理权限在这种情况下需要单独为此用户创建一个角色，现在只需要把用户加入有该权限的组中即可。同时，避免了因为使用组造成的管理不便。

![permissionModel3](https://raw.github.com/pi-asset/image/master/permission/permissionModel3.jpg)

## Permission Management Design
权限管理都在operation->system下进行，包括对角色、权限、用户的管理。

### Role Management
角色分前台角色和后台角色，一个用户可以具有多个角色，角色之间没有继承关系。<br>
功能
- 添加角色 添加前台、后台角色
- 删除角色 只能删除用户创建的角色，系统自带角色不能删除或修改，只能编辑其权限
- 修改角色的title
- 修改某角色的权限 跳转到权限管理页面，只能编辑当前角色的权限，其他角色的权限显示但无法编辑
- 添加/删除角色内的用户

每个用户创建时都会自动分配前台角色member，不能删除该角色

### Permission Management
权限区分前后台，前台角色只有前台权限，后台角色也只有后台权限。权限管理按照模块划分。

前台：<br>
每个模块都有总入口，控制用户是否具有查看和管理两种权限，如果关闭，其他权限依然可以编辑，但是无法生效<br>
各模块权限包括模块自己定义的、callback和区块权限

后台：<br>
后台权限包括operation和setting下的各项权限<br>
其中operation下的权限每个模块分别控制，setting下的权限在system->site中统一控制

可批量分配权限。

### User Management
包括基本信息查看、添加、修改、删除、过滤用户功能。<br>
添加、修改单个用户信息时可以编辑用户具有的角色信息，默认分配的member角色不能删除。不提供批量操作。
