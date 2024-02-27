## Hey there 👋🏾

```php
<?php

namespace App\Developer;

use App\SocialMedia\SocialAccountInterface;
use App\SocialMedia\LinkedInAccount;
use DateTimeImmutable;

/**
 * @requires PHP 8.3
 */
#[AsHuman]
final class GaborReszler extends BackendDeveloper implements LaravelDeveloperInterface
{
    use Laravel, MySQL, MariaDB;

    public const string FIRST_NAME = 'Gabor';
    public const string LAST_NAME = 'Reszler';
    
    public function __construct(
        public string $currentCountry = 'Hungary',
        public string $currentCity = 'Budapest',
        public DateTimeImmutable $birthDate = new DateTimeImmutable('1995-04-13'),
        public string $email = 'hello@gaborreszler.dev',
        public ?string $currentCompany = null,
        private array $previousCompanies = [
            'VTL Design'    => 'Full-stack web developer',  // https://vtldesign.hu
            'Cartographia'  => 'Junior web developer',      // https://cartographia.hu | https://funiq.hu
        ],
    ) {}
    
    public function getLinkedIn(): SocialAccountInterface
    {
        return new LinkedInAccount('https://linkedin.com/in/gaborreszler');
    }
    
    public function isLookingForAJob(): bool
    {
        if (is_null($this->currentCompany)) {
            return true;
        }
    
        return false;
    }
    
    public function isOpenForFreelanceWork(): bool
    {
        if ($this->isLookingForAJob()) {
            return true;
        }
    
        return false;
    }
    
    /**
     * @return array<string, string>
     */
    public function getPreviousCompanies(): array
    {
        return $this->previousCompanies;
    }
}
```
