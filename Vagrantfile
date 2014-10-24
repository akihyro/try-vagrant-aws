#=======================================================================================================================
# Vagrant 設定
#=======================================================================================================================

Vagrant.configure(VAGRANTFILE_API_VERSION = "2") do |config|

  # Box
  #   => Vagrant はBoxがないとダメなのでダミーを使う。
  config.vm.box = 'vagrant-aws-dummy'
  config.vm.box_url = 'https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box'

  # AWS
  config.vm.provider :aws do |aws, override|

    # アクセスキー
    #   => 事前に環境変数で定義しとく。
    aws.access_key_id = ENV['AWS_ACCESS_KEY_ID']
    aws.secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']

    # AMI
    #   => Amazon Linux AMI x86_64
    aws.ami = 'ami-4985b048'

    # インスタンスタイプ
    #   => 取り敢えず小さいので。
    aws.instance_type = 't2.micro'

    # タグ
    #   => Name: 好きな名前。
    #            AWS管理コンソールのインスタンス一覧にも表示される。
    aws.tags = {
      'Name' => 'try-vagrant-aws',
    }

    # リージョン
    #   => アジアパシフィック (東京)
    aws.region = 'ap-northeast-1'

    # サブネットID
    #   => 事前に作ったサブネットのID。
    #   => VPC環境でない場合は不要だと思う。
    aws.subnet_id = 'subnet-b3829ec7'

    # パブリックIPアドレス
    #   => 割当てる。
    #   => VPC環境でない場合は不要だと思う。
    aws.associate_public_ip = true

    # キーペア
    #   => 事前に作ったキーペア。
    aws.keypair_name = 'try-vagrant-aws'

    # セキュリティグループ
    #   => 事前に作ったセキュリティグループ。
    #   => VPC環境の場合は、名前ではなくIDで指定する。
    aws.security_groups = [ 'sg-800ac0e5' ]

    # SSH接続情報
    #   => ユーザ名と秘密鍵のパス。
    #   => pty = true は、 Amazon Linux で sudo 出来るようにごにょごにょ。
    override.ssh.username = 'ec2-user'
    override.ssh.private_key_path = '~/.ssh/try-vagrant-aws.pem'
    override.ssh.pty = true

    # Chef
    override.omnibus.chef_version = :latest
    override.vm.provision :chef_solo do |chef|
      chef.custom_config_path = 'Vagrantfile.chef'
      chef.run_list = [
        'sl',
      ]
    end

  end

end
