com-bilein-filter.jar
΢��֤��¼��������˵��
������ҳ��΢��֤��¼��������:
1������ȷ��sis_labor.properties�����ļ��Ƿ���������ɡ�
2����web.xml�����ù����������ص�¼·�������ҽ����ص�¼·���Ĺ�����ӳ����LoginFilter.java�С�
3����web.xml�����ù����������ػص�����·�������ҽ��ص�����·���Ĺ�����ӳ����CallbackFilter.java�С�
4��������ͷ�л�ȡ���ص�����õ���ѧ���ţ����е�¼��

### ��ҳ��΢��֤��¼����ṹ ###
    |-- com.bilein.filter
    |   |-- LoginFilter.java     ## ��½���ع����� ##
            ����:doFilter()      ���˵�¼��ַ����������
                 1.��ȡ�����ļ�������Sis.java
                 2.����Ϣͷ��Session�����ȡѧ����
                 3.û�л�ȡ������װ������
                   ��ȡsignin.httlҳ�棬���ɶ�ά��ҳ�棬����Ӧ
                 4.�����ȡ����ѧ���ţ�uniqueNo���������Ϣͷ��
                   ת�����ɹ���¼��ַ��
                   ����ModifyHttpServletRequestWrapper.java

    |   |-- CallbackFilter.java  ## �ص���������� ##
            ����:doFilter()      ���˻ص���ַ����������
                 1.��ȡ��Ӧ����������У�飬
                 2.��ȡУ����������ExcuteUtil,java
                 3.�ڽ���л�ȡѧ����ʧ�ܣ��������ɶ�ά����е�¼
                 4.��ȡѧ���ųɹ��������session������ͷ
                 5.ת�����ɹ���¼��ַ

    |   |-- SigninUtil.java      ## ��ҳ�˵�¼������ ##
            ����:signin()               ��װ�����������ز�������
            ����:getString(ҳ��·��)   ���ݴ�����·����ȡ�ļ�Ϊ�ַ���

    |   |-- signin.httl          ## ��ά������ҳ�� ##

    |-- system.lib  �������
    |   |-- Sis.java
            ����:getInstance(�ļ���)   ��ȡ�����ļ�����ʼ��������
            ����:get(������)           ��ȡ�ļ�������ֵ

    |-- utils.handle �������
    |   |-- ModifyHttpServletRequestWrapper.java  ������ͷ�������            ����:putHeader(������������ֵ); ������ͷ�������

    |-- eu.jar
    |   |-- com.bilein.handle
    |       |-- ExcuteUtil.java
                ������checkClientAuth(); У����ݣ�����ȡѧ����

    |-- resources(��Ŀ�ĸ�Ŀ¼)
        |-- sis_labor.properties  �����ļ�
	        `-- urlHead           ΢��֤��ַ
            `-- appid             Ӧ�ñ�ʶ
            `-- tokenKey          ����
            `-- aeskey    	      ��Կ
            `-- clienthost        ����Ŀ��ַ
	        `-- signinurl         ��ҳ����Ҫ���صĵ�¼��ַ
	        `-- signinSuccess     ��ҳ�˵�¼�ɹ���ַ
	        `-- callback          ��ҳ����֤�ص���ַ
            `-- title             ���ɵĶ�ά��ҳ�����


����΢�Ŷ�΢��֤��¼��������:
1������ȷ��sis_labor.properties�����ļ��Ƿ���������ɡ�
2����web.xml�����ù�����������΢�Ŷ˵�¼·�������ҽ����ص�¼·���Ĺ�����ӳ����WCLoginFilter.java�С�
3����web.xml�����ù����������ػص�����·�������ҽ��ص�����·���Ĺ�����ӳ����WCCallbackFilter.java�С�
4��������ͷ�л�ȡ���ص�����õ���ѧ���ţ�uniqueNo�������е�¼��


### ΢�Ŷ�΢��֤��¼����ṹ ###
    |-- com.bilein.filter
    |   |-- WCLoginFilter.java     ## ��½���ع����� ##
            ����:doFilter()      ���˵�¼��ַ����������
                  1.��ȡ��Ӧ����������У�飬
                 2.��ȡУ����������ExcuteUtil,java
                 3.�ڽ���л�ȡѧ����ʧ�ܣ��������ɶ�ά����е�¼
                 4.��ȡѧ���ųɹ���uniqueNo����
                   �����session������ͷ����ת�����ɹ���¼��ַ

    |   |-- WCCallbackFilter.java  ## �ص���������� ##
            ����:doFilter()      ���˻ص���ַ����������
                 1.��ȡ��Ӧ����������У�飬��ȡУ����
                 2.�ڽ���л�ȡѧ����ʧ�ܣ���Ӧ������ʾ
                 3.��ȡѧ���ųɹ���uniqueNo����
�����session������ͷ����ת�����ɹ���¼��ַ

    |   |-- WCSigninUtil.java      ## ��ҳ�˵�¼������ ##
            ����:generateUrl()      ����url�ض���������

    |-- system.lib  �������
    |   |-- Sis.java
            ����:getInstance(�ļ���)   ��ȡ�����ļ�����ʼ��������
            ����:get(������)           ��ȡ�ļ�������ֵ

    |-- utils.handle  �������
    |   |-- ModifyHttpServletRequestWrapper.java ������ͷ�������
����:putHeader(������������ֵ); ������ͷ�������

    |-- eu.jar   �������
    |   |-- com.bilein.handle
    |       |-- ExcuteUtil.java
                ������generateAuthUrl(); ��װ��������url

    |-- resources(��Ŀ�ĸ�Ŀ¼)
        |-- sis_labor.properties  �����ļ������÷���֮ǰ��ȷ��������ȷ
	        `-- urlHead           ΢��֤��ַ
            `-- appid             Ӧ�ñ�ʶ
            `-- tokenKey          ����
            `-- aeskey    	      ��Կ
            `-- clienthost        ����Ŀ��ַ
            `-- wccallback    	  ΢�Ŷ˵�¼ʱ�ص���ַ
	        `-- wcsuccessurl      ΢�Ŷ���֤�ɹ���ת��ַ



