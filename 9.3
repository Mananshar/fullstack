#!/bin/bash
sudo apt update -y
sudo apt install -y nodejs npm git awscli unzip
git clone https://github.com/yourusername/your-backend-repo.git /home/ubuntu/backend
cd /home/ubuntu/backend
npm install
nohup node server.js &
aws ec2 authorize-security-group-ingress --region us-east-1 --group-name your-security-group --protocol tcp --port 3000 --cidr 0.0.0.0/0
cat > main.tf <<'EOF'
provider "aws" { region = "us-east-1" }
resource "aws_security_group" "allow_all" {
  name = "allow_all"
  ingress { from_port = 0 to_port = 65535 protocol = "tcp" cidr_blocks = ["0.0.0.0/0"] }
  egress { from_port = 0 to_port = 65535 protocol = "tcp" cidr_blocks = ["0.0.0.0/0"] }
}
resource "aws_instance" "backend" {
  ami = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  security_groups = [aws_security_group.allow_all.name]
  tags = { Name = "Backend Server" }
  user_data = <<-EOT
    #!/bin/bash
    sudo apt update -y
    sudo apt install -y nodejs npm git
    git clone https://github.com/yourusername/your-backend-repo.git /home/ubuntu/backend
    cd /home/ubuntu/backend
    npm install
    nohup node server.js &
  EOT
}
resource "aws_lb" "app_lb" {
  name = "app-lb"
  internal = false
  load_balancer_type = "application"
  security_groups = [aws_security_group.allow_all.id]
  subnets = ["subnet-xxxxxxxx", "subnet-yyyyyyyy"]
}
resource "aws_lb_target_group" "target_group" {
  name = "backend-target-group"
  port = 3000
  protocol = "HTTP"
  vpc_id = "vpc-xxxxxxxx"
}
resource "aws_lb_listener" "listener" {
  load_balancer_arn = aws_lb.app_lb.arn
  port = "80"
  protocol = "HTTP"
  default_action { type = "forward" target_group_arn = aws_lb_target_group.target_group.arn }
}
EOF
terraform init
terraform apply -auto-approve
npm install -g serve
aws s3 mb s3://your-react-app-bucket
npm run build
aws s3 sync build/ s3://your-react-app-bucket --delete
aws cloudfront create-distribution --origin-domain-name your-react-app-bucket.s3.amazonaws.com
