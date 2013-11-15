# Rails Server monitored by bluepill


## Install Packages

```
apt-get update
apt-get install git
apt-get install ruby1.9.3
apt-get install postgresql libpq-dev
apt-get install build-essential g++
apt-get install nodejs
```

## Configuring the Rails App

```
git clone https://github.com/JumpstartLab/today.git /sites/today
```

```
cd /sites/today
```

Open the `Gemfile`:

* remove `ruby '2.0.0'`
* add `gem 'thin'`

```
gem install bundler
bundle
```

Create the database user, tables and seed data

```
su postgres -c "createuser root -s"
rake db:create db:migrate import
```

Run the server

```
thin start
```

## Configuring the Service

```
gem install bluepill
```

Copy the `sites/today/blue.pill` to the `/sites/today/blue.pill`

Copy the `etc/init.d/bluepill` file to `/etc/init.d/bluepill`

```
chmod a+x /etc/init.d/bluepill
chmod g+x /etc/init.d/bluepill
chmod o+x /etc/init.d/bluepill
```

Register and enable the service at the appropriate runlevels:

```
update-rc.d bluepill defaults
update-rc.d bluepill enable
```

## View Results

This runs the rails server on port 3000 it should have the rails site visible
at something like `http://162.243.150.57:3000/`

