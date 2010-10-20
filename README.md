See pod for documentation, in lib/Mojolicious/Plugin/BasicAuth.pm

# Installation

cpan Mojolicious::Plugin::BasicAuth

# Source

git clone git://github.com/tempire/mojolicious-plugin-basicauth.git

# Usage

## Callback

	use Mojolicious::Lite;

	plugin 'basic_auth';

	get '/' => sub {
		my $self = shift;

		my $callback = sub {
			return 1
				if $_[0] eq 'username'
				and $_[1] eq 'password';
		};

		$self->render_text('denied') 
			if ! $self->basic_auth( realm => $callback );

		$self->render_text('ok!');
	};

	app->start;

## Alternate usage

		return unless $self->basic_auth( realm => user => 'pass' );
		
		# User is optional:
		# $self->basic_auth( realm => 'pass' );

(See Mojolicious::Plugin::BasicAuth POD for more advanced usage)

# Credits

* Sebastian Riedel for Mojolicious
  http://github.com/kraih/mojo.git

* Viacheslav Tykhanovskyi for spreading the love over IRC

* Both of the above for making #mojo a much less abrasive
  place than #catalyst
