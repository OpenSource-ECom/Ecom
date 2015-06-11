#API authorization is broken #3485

###건의자(julen)
The API shipped in current stable (2.5.1) claims that in order to avoid all users access or alter data they are not meant to, the Pootle API checks if the visitor has enough permissions to perform the requested actions on the resources. The permissions used for these checks are the same permissions used in Pootle for regular users.

The API resources in Pootle are using Tastypie's own DjangoAuthorization class for authorization purposes, ProjectResource for instance. This class in turns integrates with Django's built-in permissions, but the problem is Pootle uses custom authorization mechanisms, and permissions are not handled the same way as in Django. Therefore any API resource using DjangoAuthorization as an authorization class is broken.

To fix this it's necessary to create and use an authorization class that truly checks Pootle's permission system.

API는 현재 안정적인 (2.5.1)에 선적되는 모든 사용자 또는 변경 데이터에 액세스 하는 것을 피하기 위해, 만약 방문객이 충분한 사용 권한을 수행할 수 있는 그들은 Pootle API점검하기 위한 의도가 아니다고 주장하고 있습니다. 이러한 검사에 사용되는 권한은 일반 사용자를위한 Pootle에서 사용되는 동일한 권한입니다.

Pootle에서 API 리소스 권한 부여 목적으로 사용하고 있습니다. 예를 들어 ProjectResource에 대한 Tastypie 자신의 DjangoAuthorization 클래스와 같이. 차례대로 클래스는 django에 내장 된 권한을 통합합니다. 그러나 문제는 Pootle 사용자 정의 인증 메커니즘을 사용하고, 권한은 장고에서와 동일한 방식으로 처리되지 않습니다. 따라서 인증 클래스로 DjangoAuthorization를 사용하여 API 자원이 끊어집니다.

이 문제를 해결하려면 그것을 만들고 진정으로 Pootle의 권한 시스템을 확인하는 권한 클래스를 사용할 필요가있는것 같습니다.